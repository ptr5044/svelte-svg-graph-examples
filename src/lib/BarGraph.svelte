<script>
  import { onMount } from "svelte";
  const data = [30, 86, 168, 281, 303, 365];
  const height = 200;
  const width = 500;

  const barHeight = 20;
  const barOffset = 3;
</script>

<svg {width} {height}>
  {#each data as val, i}
    <g class="bar">
      <text y={i * 20 + i * barOffset}>heyy</text>
      <rect width={val} height={barHeight} y={i * 20 + i * barOffset} />
    </g>
  {/each}
</svg>

<style>
  .bar rect {
    transform: translateX(50px);
  }

  .bar text {
    transform: translateY(15px);
  }
</style>
