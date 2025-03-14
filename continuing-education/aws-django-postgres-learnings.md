# Notes on AWS Django PostgreSQL

An opportunity to work on a python-based project has landed at my desk.

Rapidly ramp-up understanding of a Django project with Postgres DB that can be deployed to Amazon AWS.

- Overview and summarize.
- Point out key aspects when discovered.
- Details are less important.
- Add references as appropriate.

## AWS Production Deployment: RDS for PostgreSQL

RDS: AWS-Managed Relational DB Services in the cloud.

Steps:

1. AWS Account
1. Launch RDS instance
1. Configure DJango
1. Migrate DJango model(s)

## AWS RDS for Postgres

Cost:

- Free Tier is __Free for 12 months__.
- After 1 year __pay as you go__.
- Limited to: 750 hrs on instance, 20 GiB SSD, 20 GB backup (manual or automatic).

Create Options:

- Standard: Manual configuration of all options (availability, security, backups, maintenance).
- Easy: Best-practice configuration options are applied.

Versions:

- Latest version recommended.
- Additional cost for support of back-version Postgres instances.

Tiers:

- Production: High availability and performance.
- Dev/Test: Outside of production.
- Free tier: Develop new apps, test existing, or for training.

Note: Single and multi-instance deployments can be selected with non-free tiers.

Administration:

- Can set specific specific credentials.
- Can allow AWS Secrets Manager to manage.

Instance Sizing:

- This is the (VM/Container) size in terms of CPU, RAM, and Network.

Storage Type:

- SSD
- Magnetic
- Amount: Min 20 GiB, Max 6 TB
- Autoscaling is enabled by default and is configurable

Connectivity:

- Compute Resource: AWS-managed connection option.
- VPC (Virtual Private Cloud): A virtual networking environment.
- Public Access: Enable or disable a public IP to the DB, bounded by VPC.
- VPC Firewall: Use a default or configure custom settings.
- Proxy: Optional RDS Proxy using a Key from an IAM role and Secrets Manager.
- Certificate Authority: Optional but recommended. One is provided by default.
- Additional Configuration: Set the __Database Port__ for app connections.

Note: VPC Firewall could be configured using a New Security Group to enable a named Zone for your other apps to access the DB.

Database Auth:

- Password Auth.
- Password and IAM Auth.
- Password and Kerberos Auth.

Monitoring:

- Advanced: 15 months of performance history and CloudWatch App Signals integration.
- Basic: 7 days of performance history. Pay for more.
- There are even more settings that are advanced and specialized-case, none of which are important at this level of investigation.

Note: There are __performance insights__ and __kms key id__ configuration items that I skipped over in this review.

Additional Configuration:

- DB Name: __Set one of the DB will not work__. Avoid possible reserved names/keywords like `first`, and special characters like dash `-` or underscore `_` (probably more).
- Parameter Group.
- Backup: Automated, retention period, windows, snapshots, encryption.
- Maintenance: Minor version upgrades allowed by default. Window can be chosen or not.

Add-Ons:

- ElastiCache Cluster: Improve performance through paid scale-up service.
- RDS Proxy: Pay to pool and share DB connections for resiliency.

## DJango Settings

Connect to RDS:

- See [DJango Database Settings](https://docs.djangoproject.com/en/dev/ref/settings/#databases)
- JSON configuration file `settings.py`
- Defines: DATABASES object.
- Properties are: ENGINE (DTO package), NAME (database name), USER, PASSWORD, HOST .

## About DJango

Ref: [Django Project 5.1 Tutorial Part 1](https://docs.djangoproject.com/en/5.1/intro/tutorial01/)

- Create new django ~~site~~ Project: `django-admin startproject {packageName} {projectDir}`
- Manage.py: Interact with Django project.
- Python Package: Named after the 2nd argument `{projectDir}` and contains actual package files for your poject. Also is the __base__ name for all project references.
- `__init__.py`: ID's this as a Python package.
- `settings.py`: Configuration for this project.
- `urls.py`: Declares endpoint URLs.
- `asgi.py`: ASGI web server entrypoint.
- `wsgi.py`: WSGI web server entrypoint.

Launch Django project: `python manage.py runserver`

Project versus App:

- Project contains configuration and files to define an App.
- An App does something.
- Projects can contain one or more Apps.
- An App can be in one or more Projects.

Create An App:

- `python manage.py startapp {appName}`
- Creates the Django App directory structure.
- Deploys Django App files.

Routing:

- Always use `include()` method to build paths.
- __Never__ use `include()` to change or update `admin.site.urls` default admin site.

## Djange Databases

Databases:

- Configured in `settings.py`
- SQLite (default).
- PostgreSQL: Requires additional DJango package from PIP.
- MySql/MariaDB
- Others
- Other "installed apps" in `settings.py` require at least one DB table.
- Use `python manage.py migrate` to trigger a migration and enable "installed apps" to use the configured database.

_Note_: Only "installed apps" are affected by the `migrate` command. Change the app listing(s) then run `migrate` to ensure they are included in DB access.

Config Settings:

- See `manage.py` for what settings it will rely on.
- Declare the app and settings.py file using `os.environ.setdefault("DJANGO_SETTINGS_MODULE", {sitename.settings})` to point to a a specific settings file. The default is "mysite.settings".

Create Models:

- These define the database layout.
- Also add metadata about the layout.
- Migrations will be derived from Model definitions.
- Django generates DB schema and python API to access the object in the DB.

Activate Models:

- Update the parent project `settings.py` to include the child project and its models by adding the namespace to `INSTALLED_APPS` array.
- See: the child project's `apps.py` for the target namespace as a class name i.e. `class MyappConfig(AppConfig): ...`
- Execute `python manage.py makemigrations {title}` and output should indicate the child Project's models (tables) were created without error.
- Primary Keys (PK) are added automatically to each table.
- PK definitions can be edited prior to migration.
- Foreign Keys `_id` are also automatically added and can be configured prior to migration.

> Manage.py MakeMigrations is synonymous with Entity Framework Core's migration tools and operations. The Migration code generation defines the DB table creation and property definitions.

Tip: use `python manage.py check` to get "what if" output with making any changes.

Execute `python manage.py migrate` to implement the changes.

Migration Process:

1. Change models in `models.py`
1. Run `python manage.py makemigrations` to generate the migration code from the models.
1. run `python manage.py migrate` to apply changes to the DB schema.

Use a Django Management Shell

- `python manage.py shell`
- Imports settings in `config.py` for app-level context while in shell.
- Enables interactive operations against the database and API.

> This is a simple and powerful way to sanity-check the model definitions and schema after a migration.

Relationships:

- Identified in the Django Manager InteractiveConsole as "__" (double underscore).
- Similar to "dot access" to instance fields and functions.
- [About Model Relations](https://docs.djangoproject.com/en/5.1/ref/models/relations/)
- [DB Reference: Field Lookups](https://docs.djangoproject.com/en/5.1/topics/db/queries/#field-lookups-intro)
- [DB Reference: Queries](https://docs.djangoproject.com/en/5.1/topics/db/queries/)

## DJango Administration

Configure Admin User: `python manage.py createsuperuser`

Register Models with Admin API:

- Add `from .models import {modelName}`
- Add `admin.site.register({modelName})`

## DateTime, Python, and Django

Python and Django each have their own DateTime handling modules:

- `datetime`: Python. Enables creating and manipulating datetime instances.
- `django.utils.timezone`: Django. Time-zone utilities.
