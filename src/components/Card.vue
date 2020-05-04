<template>
<div id='card'>
  <p>Source: {{card.source}}</p>
  <p>Salary: {{punctuate(card.value)}}</p>
  <p>Title: {{card.title}}</p>
  <p v-if='card.percentile'>Percentile: {{card.percentile}}</p>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: ['card'],
  methods: {
    punctuate (num) {
      return `$${(num)},000`
    }
  }
}
</script>

<style>
#card {
  max-width:250px;
  width: 60%;
  margin: 0 auto;
  padding: 0.5em;
  background: rgba(110,110,110,0.15);
  border-radius: 7px;
  font-family: 'Noto Sans';
}

p {
    margin: 5px;
}
</style>
