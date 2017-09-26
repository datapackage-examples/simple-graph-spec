This is an example dataset, that demonstrates how to build the simple and nice graphs using the "Simple Graph Spec". We are using CBOE Volatility Index (VIX) time-series dataset for 2015-2016 as an example to create line and bar charts.

## Views

We assume that you are familiar with what [datapackage.json][datapackage.json] is and its specifications.

To create graphs for your tabular data, the `datapackage.json` should include the `views` attribute that is responsible for visualizations.

"Simple Graph Spec" is the quickest and easiest way to build a graph. To use it, inside `views` you should set `specType` to `simple` and define some graph specifications in `spec` property. See example `datapackage.json`:

```
{
  "name": "simple-graph-spec",
  "title": "Simple Graph Spec Tutorial",
  "sources": [{
    "name": "CBOE VIX Page",
    "web": "http://www.cboe.com/micro/vix/historical.aspx"
  }],
  "resources": [
    {
      "name": "vix-daily",
      "path": "data/vix-daily.csv",
      "format": "csv",
      "mediatype": "text/csv",
      "schema": {
        "fields": [
          {
            "name": "Date",
            "type": "date",
            "description": ""
          },
          {
            "name": "VIXOpen",
            "type": "number",
            "description": ""
          },
          {
            "name": "VIXHigh",
            "type": "number",
            "description": ""
          },
          {
            "name": "VIXLow",
            "type": "number",
            "description": ""
          },
          {
            "name": "VIXClose",
            "type": "number",
            "description": ""
          }
        ],
        "primaryKey": "Date"
      }
    }
  ],
  "views": [
    {
      "name": "simple-view-line",
      "title": "tutorial-on-simple-views-line",
      "resources": ["vix-daily"],
      "specType": "simple",
      "spec": {
        "type": "line",
        "group": "Date",
        "series": ["VIXHigh", "VIXLow"]
      }
    },
    {
      "name": "simple-view-bar",
      "title": "tutorial-on-simple-views-bar",
      "resources": ["vix-daily"],
      "specType": "simple",
      "spec": {
        "type": "bar",
        "group": "Date",
        "series": ["VIXOpen", "VIXOpen", "VIXHigh", "VIXLow"]
      }
    }
  ]
}
```

<br>

Only 3 properties enough to define graph specifications inside `spec` property:

<table class="table table-bordered table-striped resource-summary">
  <thead>
   <tr>
     <th>Attribute</th>
     <th>Type</th>
     <th>Description</th>
   </tr>
  </thead>
  <tbody>
    <tr>
      <th>type</th>
      <td>String</td>
      <td>line, bar, pie (defaults to line)</td>
    </tr>
    <tr>
      <th>group</th>
      <td>String</td>
      <td>Field name, that will be used as abscissa (usually date field)</td>
    </tr>
    <tr>
      <th>series</th>
      <td>Array</td>
      <td>Field name(s) that will be used as ordinate</td>
    </tr>
  </tbody>
</table>

You can define multiple views for your dataset. For example, to display line graph as presented above, we defined graph `type` to be a `line`:

```
  ...
  "spec": {
    "type": "line",
    ...
  }
```

Similarly to display bar chart we've used `bar` type:

```
  ...
  "spec": {
    "type": "bar",
    ...
  }
```

We use `Date` field to display data over time, by setting `group` attribute to the field name:

```
  ...
  "spec": {
    ...
    "group": "Date",
    ...
  }
```

You can set any number of fields to display in `series` attribute as an array:

```
  ...
  "spec": {
    ...
    "series": [
      "VIXHigh",
      "VIXLow"
    ]
 }
```

In our case we've displayed line graph for `VIXHigh` and `VIXLow` and similarly, in the bar chart, we use all four series and all of them are presented in chart.

Outside of `spec` attribute there are some other important parameters to note:

<table class="table table-bordered table-striped resource-summary">
  <thead>
   <tr>
     <th>Attribute</th>
     <th>Type</th>
     <th>Description</th>
   </tr>
  </thead>
  <tbody>
    <tr>
      <th>name</th>
      <td>String</td>
      <td>Unique identifier for view within list of views (lines 51 and 62)</td>
    </tr>
    <tr>
      <th>title</th>
      <td>String</td>
      <td>Title for the graph (lines 52 and 63)</td>
    </tr>
    <tr>
      <th>resources</th>
      <td>Array</td>
      <td>Data sources for this spec. It can be either resource name or index. By default it is the first resource (lines 53 and 64)</td>
    </tr>
    <tr>
      <th>specType</th>
      <td>String</td>
      <td>Available options: simple, vega, plotly <strong>(Required)</strong></td>
    </tr>
  </tbody>
</table>

[datapackage.json]: http://specs.frictionlessdata.io/data-package/
