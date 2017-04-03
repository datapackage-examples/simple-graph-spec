# Tutorial datapackage on Simple Views

This repo includes a data package without views. You can clone and then publish it, but there will be no graphs. To quickly and easily add a graph follow instructions below:

* Clone the repo and edit `datapackage.json`

```
$ git clone https://github.com/anuveyatsu/tutorial-datapackage.git
```

`views` MUST be an array. Each entry in the array MUST be an object. This object MUST follow the Data Package View specification set out here.:

A View MUST have the following form:

```
{
  // generic metadata
  "name": "..."   // unique identifier for view within list of views. (should we call it id ?)
  "title": "My view" // title for this graph

  // data sources for this spec
  "resources": [ resource1, resource2 ]  

  "specType": "" // one of simple | plotly | vega
  // graph spec
  "spec":
}
```

Now edit `datapackage.json` - add a new attribute called `views`:

```
{
  ...
  "resources": [
    ...
  ],

  "views": [
    {
      "name": "simple-view",
      "title": "tutorial-on-simple-views",
      "resources": [0], // 0 is an index of a resource - it is by default pointing to 0th resource
      "specType": "simple",
      "spec": {
        "type": "line",
        "group": "Date",
        "series": ["VIXHigh", "VIXLow"]
      }
    }
  ]

}
```
