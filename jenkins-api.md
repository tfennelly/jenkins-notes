#Jenkins API

Jenkins has a HTTP based API that can be accessed on the Jenkins instance through the `/api/` subpath.  Docs are available on your Jenkins instance if you can locate the "REST API" link on the console.

##Data Format
You can request XML or JSON by suffixing the URL path with "xml" or "json" e.g.

```
http://localhost:8080/jenkins/api/xml
```
Or
```
http://localhost:8080/jenkins/api/json
```

## Narrowing/Filtering the returned Data Graph
You can reduce the amount of data returned in one of 2 ways:

1. __XPath Query__: Add an `xpath` query on the request URL.
1. __'tree' Query__: Add a `tree` query on the request URL.

Making a request on the JSON API endpoint without either of these query parameters returns the full model.  Lets take JSON as the example (note the query param for pretty printing):

```
http://localhost:8080/jenkins/api/json?pretty=true
```
That query would return a structure like the following:

```json
{
  "assignedLabels" : [
    {

    }
  ],
  "mode" : "NORMAL",
  "nodeDescription" : "the master Jenkins node",
  "nodeName" : "",
  "numExecutors" : 5,
  "description" : null,
  "jobs" : [
    {
      "name" : "Test XXX",
      "url" : "http://localhost:8080/jenkins/job/Test%20XXX/",
      "color" : "blue"
    }
  ],
  "overallLoad" : {

  },
  "primaryView" : {
    "name" : "All",
    "url" : "http://localhost:8080/jenkins/"
  },
  "quietingDown" : false,
  "slaveAgentPort" : 0,
  "unlabeledLoad" : {

  },
  "useCrumbs" : false,
  "useSecurity" : false,
  "views" : [
    {
      "name" : "All",
      "url" : "http://localhost:8080/jenkins/"
    },
    {
      "name" : "Random thing",
      "url" : "http://localhost:8080/jenkins/view/Random%20thing/"
    }
  ]
}
```

If we were only interested in getting the "mode" element of the graph, we can narrow the result by adding the `tree` query param as follows:

```
http://localhost:8080/jenkins/api/json?pretty=true&tree=mode
```

Which would return:

```json
{
  "mode" : "NORMAL"
}
```
More powerful `tree` query expressions are support, so it's worth while checking out the docs.

__Note__: I've noticed what seemed to be strange behaviour in the API when using the `tree` parameter e.g. if I query the above dataset for "primaryView" I get back an empty object.  I tried playing with the `depth` parameter, but it didn't seem to have an effect.

###'depth' query parameter
You can further control the amount of data returned in a response by adding a `depth` paramter to the request.
