#Development Notes
Some random notes.

##Hot Reload of Changes
Use the `maven-jenkins-dev-plugin` plugin to run Jenkins when developing.  This will hot reload all your changes as you make them (including Jelly script changes).

Run a full build of Jenkins (`mvn clean install`).  Then, from the `war` folder, run:

```
mvn org.jenkins-ci.tools:maven-jenkins-dev-plugin:run
```

Creating a command line alias for this obviously makes it a bit easier to run.

##Debugging
If you need to debug your running Jenkins, simply set the debugger options in your `MAVEN_OPTS` environment variable e.g. to debug on port 5000 set the following:

```
export MAVEN_OPTS="-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5000"
```

Once you start Jenkins with the above `MAVEN_OPTS` set, you'll be able to connect your debugger to the instance on port 5000.
