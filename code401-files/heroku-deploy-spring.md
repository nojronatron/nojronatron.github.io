# Lessons Learned Deploying Springboot to Heroku

## References

Heroku [Dev Center](https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku)

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
- or a gradlew file AND `gradle/wrapper/dragle-wrapper.jar` and `gradle/wrapper/dradle-wrapper.properties` in git repo and *not* gitignored

TODO: Take an hour to go through [this Gradle tutorial](https://learn.tomgregory.com/courses/get-going-with-gradle)

Create a plain text file at the root of your Spring project named `Procfile.` without an extention and paste in the following code:

```sh
web: java -Dserver.port=$PORT $JAVA_OPTS -jar build/libs/demo-0.0.1-SNAPSHOT.jar
```

Commit these changes to the deployable branch. In Heroku-cli, launch the webapp with `heroku open`

## Notes

Heroku detects the Java app through presence of a 'pom.xml' file.

Heroku uses OpenJDKs Heroku (heroku-18 or heroku-20) or AzulZulu (heroku-22) which are certified Java SE specification compliant.

Postgres DB is *automatically provisioned* for Java apps that have a dependency on "Postgres JDBC driver" or "pgjdbc-ng driver" in `pom.xml` which will auto-populate env variable `DATABASE_URL` for you.

## Footer

Back to root [Readme](../README.html)
