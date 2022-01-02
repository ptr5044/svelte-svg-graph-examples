<script lang="ts">
  import { onMount } from "svelte";
  const height = 200;
  const width = 500;
  const barHeight = 20;
  const barOffset = 3;

  export let barData: { label: string; value: number }[];
</script>

<svg {width} {height}>
  {#each barData as val, i}
    <g class="bar">
      <text y={i * 20 + i * barOffset}>{val.label}</text>
      <rect
        width={`${val.value}%`}
        height={barHeight}
        y={i * 20 + i * barOffset}
      />
    </g>
  {/each}
</svg>

<style>
  .bar rect {
    animation: grow 1s forwards;
  }

  .bar text {
    transform: translateY(15px);
  }

  @keyframes grow {
    0% {
      transform: translateX(60px) scaleX(0);
      opacity: 0;
    }
    70% {
      transform: translateX(60px) scaleX(1.05);
      opacity: 0.8;
    }
    100% {
      transform: translateX(60px) scaleX(1);
      opacity: 1;
    }
  }
</style>
