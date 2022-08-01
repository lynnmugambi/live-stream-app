<template>
  <div id="app">
    <SideBar></SideBar>
    <StreamCanvas></StreamCanvas>
  </div>
</template>

<script>
import SideBar from "./components/SideBar.vue";
import StreamCanvas from "./components/StreamCanvas.vue";
export default {
  name: "App",
  components: {
    SideBar,
    StreamCanvas,
  },
};
</script>

<style lang="scss">
#app {
  @apply flex flex-row;
  width: 100%;
  height: 100vh;
}
</style>
