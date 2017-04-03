This Data Package includes `views` attribute that defines data views such as graphs or tables based on the data in a Data Package. We use "Simple Graph Spec" in this Data Package, which is the quickest and easiest way to describe a graph:

<script src="https://gist.github.com/anuveyatsu/87f164d04054f82189c86559f99546e7.js"></script>

In the views spec, we use syntax called "Simple Graph Spec" - must be specified in `specType` attribute as `simple` (as in line 54). By providing only 3 attributes one can get a graph:

* `type` (string) - options are `line`, `bar` or `pie`

* `group` (string) - field name that will be used as a basis (normally it is date that is used as abscissa)

* `series` (array) - field(s) name that will be used as ordinate

In the first `view` we define graph `type` as `line` (line 56). So the first graph in this page is displaying line chart. In the second `view` we define it as `bar` (line 67), so the second graph is a bar chart.

In our data `Date` field is a primary field so we use it as `group` and we can use other fields as `series`. We use `VIXHigh` and `VIXLow` fields as `series` so in the line chart we can see two lines being rendered. Similarly in the bar chart we use three series so they are rendered on top of each other.


Outside of `spec` attribute there are some other important parameters to note:

* `name` (lines 51 and 62) - unique identifier for view within list of views.

* `title` (lines 52 and 63) - title for this graph.

* `resources` (lines 53 and 64) - data sources for this spec. It can be either resource name or index. In our example we use resource's name. By default it is the first resource.

* `specType` (lines 54 and 65) - used for defining syntax. In this demo datapackage we use `simple` (Simple Graph Spec).
