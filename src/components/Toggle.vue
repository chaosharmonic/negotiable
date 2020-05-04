<template>
  <div id='toggleContainer'>
    <button class='toggle'
      :class='activeRegion.local'
      @click='toggleSources'>Local</button>
    <button class='toggle'
      :class='activeRegion.national'
      @click='toggleSources'>National</button>
  </div>
</template>

<script>
export default {
  name: 'Toggle',
  props: ['activeRegion', 'toggleSources']
}
</script>

<style>
.toggle {
  color: inherit;
  text-transform: uppercase;
  margin: 3vh 1.5vh;
  background: none;
  padding: 1em;
  border: 1px solid white;
  border-radius: 7px;
  outline: none;
  transition: all 0.25s;
}
#toggleContainer {
  height: 10vh;
}
.inactive {
  color: rgb(150, 150, 150);
}
</style>
