# Read Class 37 Notes

Intro to Amazon S3 and S3 with Amplify.

## References

Intro to [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/Introduction.html)

About [S3 with Amplify](https://docs.amplify.aws/lib/storage/getting-started/q/platform/android/)

## Amazon S3

S3 => Simple Storage Service

Object Storage.

Scalable, Available, Secure storage, and performance.

Used for:

- data lakes
- websites
- mobile platforms and apps
- backup and restore
- archive
- enterprise apps
- IoT
- Big Data Analytics

### Storage Classes

Archival storage with Glacier.

Random-access and storage data can be stored in S3 Intelligent Tiering - 4 Tiers of access dynamically changed to get best performance.

### Storage Management

- S3 Lifecycle: Policy to manage objects for deletion or migration.
- S3 Object Lock: Prevent deletion for fixed period of time or forever.
- S3 Replication: Ensure objects are the same in different AWS Regions (latency, compliance, security, etc).
- S3 Batch Operations: Copy, LambdaFunction, Restore operations can be done in bulk on 'billions of objects'.

### Access Management

By default, S3 Buckets are 'private'.

- S3 Block Public Access: Denies public access to buckets.
- AWS IAM: Identity and Access Management. Apply to S3 Buckets as well as other resources.
- Bucket policies: Use with IAM to provide permissions settings for buckets and objects in buckets.
- S3 Access Points: Access Policies apply to data access to shared datasets.
- ACLs: Read/Write permissions and access control policies. Integrates with IAM.
- S3 Object Ownership: Disable ACLs and override with ownership rights. Bucket Owner is root of all objects.
- Access Analyzer for S3: Monitor policies and verify access rights on S3 Buckets.

### Data Processing

- S3 Object Lambda: GET requests to modify and process data. Filter, resize, redact info...etc.
- Event Notifications: Trigger SNS workflows. Also supports SQS and Lambda.

### Storage Logging and Monitoring

Automated and Manual Monitoring Tools with server access logging and AWS Trusted Advisor.

### Analytics and Insights

Storage Lens, Class Analysis, and Inventory tools.

### Strong Consistency

PUT and DELETE requests data integrity in all Buckets in all S3 Regions.

### How S3 Works

Object Storage Service, stored data in generic Buckets. Also stores metadata.

To use:

1. create a bucket
1. give it a name (cannot be changed, and there are naming rules)
1. supply a deployment region (cannot be changed)
1. upload data to the bucket as "objects"

Objects have Keys: Unique IDs for each object in the Buckets.

Versioning allows retaining multiple object versions in same bucket.

Buckets and Objects start out private. Permissions to access can be granted through:

- Bucket Policies
- IAM Policies
- ACLs
- S3 Access Points

### Buckets

Unlimited objects per bucket.

Limit 100 Buckets per account (Service Quota setting - can request more).

Access buckets using https protocol URIs.

### Objects

Fundamental entities.

Metadata is name-value pairs of info about the Objects, and includes Content-Type, modified, and other standard HTTP info.

### Keys

AKA Key Name.

Unique within a Bucket.

Object ID is derived from: Bucket, Object Key, optional Version ID, creating a data.

### S3 Versioning

Existing Objects will have `version=null` when Versioning added; new Objects will get new versioning scheme IDs.

### Bucket Policy

IAM policies.

Bucket Owners can associate policies with buckets.

Policies are JSON-based (standard across AWS!).

Wildcards are allowed in Bucket Policies.

### S3 Access Points

Named network endpoints.

Access Policies allow/deny endpoint access.

Endpoints are attached to buckets for GetObject and PutObject operations.

Access Points can be associated with a specific Virtual Private Cloud (VPC).

## ACLs

Read and Write permissions to Buckets and Objects.

Older than IAM.

Object Writers become Object Owners, by default.

ACLs are going out of style so it is safe to disable them when starting a new Bucket.

### Regions

Select a region for Bucket(s) based on:

- Latency
- Minimizing Costs
- Regulatory Requirements

Region-bound Objects "never leave the Region unless...explicitly transferred..."

### Data Consistency Model

Read-after-Write model for PUT and DELETE requests.

Single-key updates are *atomic*.

All data is replicated *within AWS datacenters* so when you query or mutate, you *cannot know which version your operation is working with*, but at least the operation will be *atomic* and not result in corruption.

*Think of it this way*: There will *always* be a slight delay as changes take a few moments to propagate through the system.

### Using With Other Services

S3 Buckets can be accessed by other AWS services:

- EC2 (Elastic Compute Cloud): Virtual Servers, managed storage, and virtual network configurations.
- EMR: Hadoop-framework data processing.
- Snow Family: Use to access storage and services in areas where internet connectivity is inconsistent.
- Transfer Family: Managed support of file transfers in/out of Amazon S3.

### Accessing S3

AWS Management Console: web-based.

AWS CLI: Teletype or script-based operations on S3 tasks.

AWS SDKs: Libraries and sample code (Java, Python, Ruby, .NET, iOS, Android, etc), supporting programmatic access to AWS services.

S3 REST API: Store and Retrive objects via this HTTP interface. Use any toolkit that support HTTP. Supports headers to additional functionality including authorization. Signatures are *required* for all requests.

### PCI DSS Compliance

Compliant with credit-card processing requirements and standards.

## S3 with Amplify

Getting Started:

1. Provision backend storage: `amplify add storage` and respond to the list of questions.
1. Push changes to cloud: `amplify push`.
1. Install Amplify Libraries into App build.gradle: `implementation 'com.amplifyframework:aws-storage-s3:1.36.1' implementation 'com.amplifyframework:aws-auth-cognito:1.26.1'`
1. Sync Gradle config with your Project.
1. Init Amplify Storage with `Amplify.addPlugin()` for each category in your App entrypoint.
1. Upload Data to your Bucket: Must have the key and data object to be uploaded. See [sample code](https://docs.amplify.aws/lib/storage/getting-started/q/platform/android/#uploading-data-to-your-bucket).

## Footer

Return to [Root README](../README.html)
