CBOE Volatility Index (VIX) time-series dataset for 2015-2016, including daily open, close, high and low. This is an example DataPackage that demonstrates usage of simple graph specifications for tabular data.

## Views

To create graphs for your tabular DataPackage, the `datapackage.json` should include the `views` attribute that defines data views. 

### Simple Graph Specifcations

We use "Simple Graph Spec" in this DataPackage, which is the quickest and easiest way to describe a graph:

<script src="https://gist.github.com/anuveyatsu/87f164d04054f82189c86559f99546e7.js"></script>

To use "Simple Graphs Spec", `specType` inside `views` atribute should be set to `simple` - line 54.

There are only 3 properties enough to define graph sepcifications. They should be set inside `spec` attribute - line 55

| attribute            | type     | Description  |
| :------------------ | :--------| :------------|
| type   | String | line, bar, pie (defaults to line)|
| group  | String | Field name, that will be used as abscissa (usually date field)|
| series | Array | Field name(s) that will be used as ordinate|

You can define multiple views for your DataPackage - In the first `view` we define graph `type` as a `line` (line 56). So the first graph above displays the line chart. In the second `view` we define it as a `bar` (line 67), so the second graph is a bar chart.

We use `Date` field to display data over time, by setting `group` attribute to the field name - line 57 and line 68. You can set any number of fields to display in `series` atribute as an array - line 58 and line 69.  In our case `VIXHigh` and `VIXLow` for first graph. Similarly, in the bar chart, we use three series, so all three are rendered in the second graph.


Outside of `spec` attribute there are some other important parameters to note:

| attribute           | type     | Description  |
| :------------------ | :--------| :------------|
| name   | String | Unique identifier for view within list of views (lines 51 and 62) |
| title  | String | Title for the graph (lines 52 and 63)|
| resources | Array | Data sources for this spec. It can be either resource name or index. By default it is the first resource (lines 53 and 64) |
| specType | String | Available options: simple, vega, plotly **Required** |
