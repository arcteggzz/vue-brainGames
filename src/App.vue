<template>
  <div id="app">
    <Controls />
    <Game v-if="gameActive"/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Controls from "./components/Controls.vue";
import Game from "./components/Game.vue";

export default Vue.extend({
  name: 'App',
  components: { Controls, Game },
  computed: {
    gameActive(){
      return this.$store.state.gameActive;
    }
  },
});
</script>

<style>
</style>
