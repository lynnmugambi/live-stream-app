<template>
  <div id="app">
    <SideBar @views="setViews($event)"></SideBar>
    <StreamCanvas :streamViews="selectedViews"></StreamCanvas>
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
  data() {
    return {
      selectedViews: [],
    };
  },
  methods: {
    setViews(data) {
      //passes selected views to the StreamCanvas for display
      this.selectedViews = data;
    },
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
