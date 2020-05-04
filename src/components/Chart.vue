<template>
    <svg
      :viewbox="chartWidth">
      <g v-for="(d, i) in dataset" :key="d.key">
        <rect
          @mouseover="renderCard(i)"
          @mouseout="removeCard()"
          :id="d.id"
          :class="d.class"
          :width="`${barWidth - 1.5}%`"
          :height="barHeight(d)"
          :x="`${barWidth * i + .75}%`"
          :y="225 - barHeight(d)" />
        </g>
      </svg>
</template>

<script>
export default {
  name: 'Chart',
  props: ['dataset', 'renderCard', 'removeCard'],
  methods: {
    barHeight (bar) {
      return bar.value * 1.5
    }
  },
  computed: {
    barWidth () {
      return 100 / this.dataset.length
    },
    chartWidth () {
      return this.dataset.length * 10
    },
    viewboxUnits () {
      return `0 0 ${this.chartWidth} 150`
    }
  }
}
</script>

<!-- Global CSS -->
<style>
  svg {
    height: 225px;
    width: 80vw;
    max-width: 700px;
    padding: 1.5vh;
    margin-top: 5vh;
    background: rgba(110,110,110,0.15);
  }
  rect {
    fill: rgb(0, 145, 90);
  }
  rect:hover {
    fill: rgb(0, 200, 65);
    transition: all 0.25s;
  }
  .lowEnd {
    fill: rgb(0, 85, 255);
  }
  .lowEnd:hover {
    fill: rgb(0, 180, 255);
  }
  #control {
    fill: rgb(200, 25, 25);
  }
  #control:hover {
    fill: rgb(255, 25, 25);
  }
</style>
