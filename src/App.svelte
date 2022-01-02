<script>
  import BarGraph from "./lib/BarGraph.svelte";
  import { barData } from "./assets/BarGraph.data";

  import LineChart from "./lib/LineChart.svelte";
  import { lineData } from "./assets/LineChart.data";
</script>

<BarGraph {barData} />
<LineChart {lineData} />
