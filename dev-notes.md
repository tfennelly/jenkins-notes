#Development Notes
Some random notes.

##Hot Reload of Changes
Use the `maven-jenkins-dev-plugin` plugin to run Jenkins when developing.  This will hot reload all your changes as you make them (including Jelly script changes).

Run a full build of Jenkins (`mvn clean install`).  Then, from the `war` folder, run:

```
mvn org.jenkins-ci.tools:maven-jenkins-dev-plugin:run
```
