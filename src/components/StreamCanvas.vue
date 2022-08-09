<template>
  <main class="stream-canvas">
    <div class="container"></div>
    <StreamOptions :views="streamViews"></StreamOptions>
    <ActionPanel></ActionPanel>
  </main>
</template>

<script>
import ActionPanel from "./ActionPanel.vue";
import StreamOptions from "./StreamOptions.vue";
export default {
  name: "StreamCanvas",
  components: { ActionPanel, StreamOptions },
  props: {
    streamViews: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style lang="scss" scoped>
.stream-canvas {
  @apply w-full my-10 mx-20 flex flex-col justify-center items-center;

  .container {
    @apply bg-black max-h-full w-full;
    aspect-ratio: 16/9;
    max-width: 1500px;
    margin-top: -60px;
  }
}
</style>