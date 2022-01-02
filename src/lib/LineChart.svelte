<script lang="ts">
  import _ from "lodash";
  import { draw, fade } from "svelte/transition";
  import { onMount } from "svelte";
  import { palette } from "../assets/ColorPalette";

  let xMultiplier = 1;
  let yMultiplier = 1;
  let xMax = 0;
  let yMax = 0;
  let points: string = "";
  let show = false;

  export let height = 200;
  export let width = 500;
  export let xMargin = 10;
  export let yMargin = 10;
  export let lineData: { x: number; y: number }[];
  export let strokeColor = palette[0];
  export let strokeWidth = 6;

  onMount(() => {
    show = true;
  });

  $: {
    xMax = _.maxBy(lineData, "x")?.x;
    yMax = _.maxBy(lineData, "y")?.y;
    xMultiplier = width / xMax;
    yMultiplier = height / yMax;

    lineData.forEach((o) => {
      points = points.concat(
        `${o.x * xMultiplier + xMargin + strokeWidth / 2}, ${
          o.y * yMultiplier - yMargin - strokeWidth / 2
        } `
      );
      console.log(points);
    });

    console.log(xMultiplier);
  }
</script>

{#if show}
  <svg {width} {height}>
    <line
      transition:fade
      x1={xMargin}
      y1={-yMargin}
      x2={xMargin}
      y2={yMax * yMultiplier - yMargin}
    />
    <line
      transition:fade
      x1={xMargin}
      y1={yMax * yMultiplier - yMargin}
      x2={xMax * xMultiplier - xMargin}
      y2={yMax * yMultiplier - yMargin}
    />
    <polyline
      {points}
      transition:draw
      stroke={strokeColor}
      stroke-width={strokeWidth}
    />
  </svg>
{/if}

<style>
  polyline {
    fill: #fff;
    stroke-linecap: round;
  }

  line {
    stroke: #37373790;
    stroke-width: 2;
  }
</style>
