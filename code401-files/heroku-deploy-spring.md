# Lessons Learned Deploying Springboot to Heroku

## Content

Set up apt with Heroku cli's latest deb:

```sh
# Run this from your terminal.
# The following will add our apt repository and install the CLI:
sudo add-apt-repository "deb https://cli-assets.heroku.com/branches/stable/apt ./"
curl -L https://cli-assets.heroku.com/apt/release.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install heroku
```

Change directory to your project root and commit any final changes.

Pull those changes to "main".

Login to Heroku (website) first, then login to Heroku CLI: `heroku login`

Update git remotes to include heroku fetch/push urls: `git remote add heroku heroku_project_url.git`

Push 'main' code to Heroku using `git push heroku main`.

Update 'system.properties' to run the app in Heroku by specification in article [Specifying a Java version](https://devcenter.heroku.com/articles/java-support#specifying-a-java-version)

## System Properties Updates

Specify java runtime version: `java.runtime.version=nn`

Recommend *not* specifying java runtime to enable automatic security updates (otherwise dev must do it and re-push).

## Gradle-specific Notes

Devcenter Heroku article [Deploying Gradle Apps on Heroku](https://devcenter.heroku.com/articles/deploying-gradle-apps-on-heroku)

Heroku supports Java Apps using Gradle that contain the following:

- build.gradle file
- settings.gradle file
- or a gradlew file AND `gradle/wrapper/gradle-wrapper.jar` and `gradle/wrapper/gradle-wrapper.properties` in git repo and *not* gitignored

TODO: Take an hour to go through [this Gradle tutorial](https://learn.tomgregory.com/courses/get-going-with-gradle)

Create a plain text file at the root of your Spring project named `Procfile.` without an extention and paste in the following code:

```sh
web: java -Dserver.port=$PORT $JAVA_OPTS -jar build/libs/demo-0.0.1-SNAPSHOT.jar
```

Commit these changes to the deployable branch. In Heroku-cli, launch the webapp with `heroku open`

## GitHub Connect Method

1. Create a new Github Repo.
1. Build your code, make sure the website and db connection works.
1. Login to Heroku (webapp) and create a new App.
1. Select Deployment Method "GitHub: Connect to GitHub".
1. If you have not connected Heroku to GitHub before you will be asked by GitHub to allow Heroku access to your Repos.
1. Type the name of the repo (or at least part of it) and below the Search your matching repo(s) will appear.
1. Click "Connect" next to the repo you want to connect this to.
1. Assuming that succeeds (a Disconnect... buton appears) scroll down to "Automatic Deploys" section and make sure the correct branch is selected (usually main).
1. Optional: Wait for CI to pass before deploy.
1. Click Enable Automatic Deploys button. A green check-mark should appear next to "Automatic deploys from (branch) are enabled".

### Notes

Instead of automatic deploys, you can configure Manual Deploy, it is just below Automatic Deploys subsection.

Setting the java compatibility in ...

TODO: Check out [section 68.1 Build](https://docs.spring.io/spring-boot/docs/1.1.4.RELEASE/reference/htmlsingle/#common-application-properties) regarding https behind a proxy.

TODO: This other reference to [Force the use of HTTPS](https://devcenter.heroku.com/articles/preparing-a-spring-boot-app-for-production-on-heroku)

Heroku detects the Java app through presence of a 'pom.xml' file, but this applies to Maven *not* Gradle.

Heroku uses OpenJDKs Heroku (heroku-18 or heroku-20) or AzulZulu (heroku-22) which are certified Java SE specification compliant.

Postgres DB is *automatically provisioned* for Java apps that have a dependency on "Postgres JDBC driver" or "pgjdbc-ng driver" in `pom.xml` which will auto-populate env variable `DATABASE_URL` for you.

## Thursday 16-Jun

[stackfellows-wip Heroku Activity](https://dashboard.heroku.com/apps/stackfellows-wip/activity)

### Stuff I Did That Seemed To Make Things Work

1. Add `system.properties` file to project root and added `java.runtime.version=17` (solves "Invalid source release")
1. Built app using `gradle build` and used `find . -name "*.jar"` to locate jar path (need to fix build cannot find JAR)
1. Add `Procfile` (no period) to project root and added `web: java -Dserver.port=$PORT -jar build/libs/app-0.0.1-SNAPSHOT.jar` (as a result of gradle build output step above) (fixes build cannot find JAR error)
1. Add postgres to Heroku via (web or) heroku-cli: `heroku addons:create heroku-postgresql:hobby-dev` (Fixes failure to connect to datasource error)
1. Added `SERVER_ERROR_WHITELABEL_ENABLED=false` to Vars (fixes Whitelabel error messages)

*Current Remaining Known Issue*: Unable to add to database (Register new user).

### Other VARs Changed

It is not clear to me whether/if any/all of these have made a difference:

- SPRING_JPA_GENERATE_DLL=true (could be a -DLL or _DLL not sure)
- SPRING_JPA_HIBERNATE_DLL_AUTO=update (could be a -AUTO or _AUTO not sure)
- SPRING_MVC_HIDDENMETHOD_FILTER_ENABLED=true

### Worth Noting

Once Heroku's postgres addon is included in the App config, the necessary VARs were added automatically by Heroku.

The automatic postgres VARs include the username and password to the postgres installation, and its path!

## References

Spring Docs: [System Environment Property Source](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/core/env/SystemEnvironmentPropertySource.html)

Heroku Dev Center: [Config Vars](https://devcenter.heroku.com/articles/config-vars)

Tom Gregory dot Com: [Get Going With Gradle Course (1 hour)](https://learn.tomgregory.com/courses/get-going-with-gradle)

Stack Overflow: [Error Connecting to PostgresQL with Spring](https://stackoverflow.com/questions/68850665/failed-connection-when-trying-for-heroku-postgresql-with-spring)

Spring dot IO guides: [Gradle](https://spring.io/guides/gs/gradle/)

Arose 13's [Heroku Spring Gradle Example](https://github.com/arose13/Heroku-Spring-Gradle_Example/blob/master/build.gradle)

Heroku Dev Central: [Secure Java Web App for Production](https://devcenter.heroku.com/articles/preparing-a-java-web-app-for-production-on-heroku)

Heroku Dev Center: [Deploying  Spring Boot Apps to Heroku](https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku)

Heroku Dev Center: [Proc File](https://devcenter.heroku.com/articles/procfile)

Heroku Dev Center: [Deploying Gradle Apps to Heroku](https://devcenter.heroku.com/articles/deploying-gradle-apps-on-heroku)

Heroku Dev Center: [Default Web Process Type for Java](https://devcenter.heroku.com/articles/java-support#default-web-process-type)

[Heroku Postgres](https://elements.heroku.com/addons/heroku-postgresql)


## Footer

Back to root [Readme](../README.html)
