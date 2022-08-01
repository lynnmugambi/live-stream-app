<template>
  <div class="stream-canvas">
    <div class="container"></div>
    <ActionPanel></ActionPanel>
  </div>
</template>

<script>
import ActionPanel from "./ActionPanel.vue";
export default {
  name: "StreamCanvas",
  components: { ActionPanel },
};
</script>

<style lang="scss" scoped>
.stream-canvas {
  @apply w-full my-10 mx-20 flex flex-col justify-center items-center;

  .container {
    @apply bg-black max-h-full w-full;
    aspect-ratio: 16/9;
    max-width: 1500px;
    margin-top: -80px;
  }
}
</style>