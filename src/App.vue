<template>
  <div id='app'>
    <h1>Average boilerplate salaries</h1>
    <Toggle
      :toggleSources='toggleSources'
      :activeRegion='activeRegion' />
    <Chart
      :dataset='chartData'
      :card=card
      :renderCard='renderCard'
      :removeCard='removeCard' />
    <Card
      v-if='card'
      :card='card' />
  </div>
</template>

<script>
import dataset from './datasets/boilerplate'
import Card from './components/Card.vue'
import Chart from './components/Chart.vue'
import Toggle from './components/Toggle.vue'
export default {
  name: 'app',
  methods: {
    toggleSources () {
      this.isLocal = !this.isLocal
      console.log(this.sources)
    },
    renderCard (index) {
      this.card = this.chartData[index]
    },
    removeCard () {
      this.card = null
    }
  },
  data () {
    return {
      currentSalary: { title: 'Boilerplate Specialist', value: 63, source: 'Current Position', id: 'control' },
      isLocal: false,
      card: null,
      dataset
    }
  },
  computed: {
    sources () {
      const { dataset, isLocal } = this

      return isLocal
        ? dataset.filter(x => x.region)
        : dataset.filter(x => !x.region)
    },
    chartData () {
      return [this.currentSalary, ...this.sources]
        .sort((a, b) => a.value - b.value)
        .map((e, i) => {
          e.key = `LV${i}`
          if (e.percentile !== 50) e.class = 'lowEnd'
          return e
        })
    },
    activeRegion () {
      let local, national
      !this.isLocal ? local = 'inactive' : national = 'inactive'

      return { local, national }
    }
  },
  components: {
    Chart,
    Toggle,
    Card
  }
}
</script>

<!-- Global CSS -->
<style>
  @import url('https://fonts.googleapis.com/css2?family=Lato');

  body {
    color: rgb(255, 255, 255);
    background: rgb(0, 0, 0);
    text-align: center;
    font-family: 'Lato';
  }
  #app {
    width: 80%;
    margin: 0 auto;
  }
  .toggle {
    color: currentColor;
    text-transform: uppercase;
    margin: 3vh 1.5vh;
    background: none;
    padding: 1em;
    border: 1px solid white;
    /* TODO: how to get rid of selection on icon? */
  }
  #toggleContainer {
    height: 10vh;
  }
  .inactive {
    color: rgb(150, 150, 150)
  }
  line {
    color: white;
  }
  text {
    fill: white;
  }

</style>
