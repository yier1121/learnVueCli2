<template>
  <div id="app">
    <header1></header1>
    <div class='tab'>
      I am a tab
    </div>
    <div class='content'>
      I am a content
    </div>    

  </div>
</template>

<script>
import header1 from './components/header/header.vue';
export default {
  name: 'App',
  components: {
    header1
  }
}
</script>

<style>

</style>
