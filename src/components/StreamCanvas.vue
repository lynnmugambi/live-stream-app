<template>
  <main class="stream-canvas">
    <!-- Display Element-->
    <div class="container" :class="parentClass">
      <div v-if="type === 'shared'" :class="viewOrientation">
        <div class="inner"></div>
      </div>
      <div v-else :class="viewOrientation"></div>
    </div>
    <StreamOptions
      :views="streamViews"
      @orientViews="viewOrientation = $event"
    ></StreamOptions>
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
  data() {
    return {
      type: "",
      viewOrientation: "",
      parentClass: "",
    };
  },
  watch: {
    streamViews(newViews) {
      // sets default orientation in display element when sources are set initially
      if (newViews.includes("Screenshare") && newViews.length < 2) {
        this.viewOrientation = "screenshare";
      }
      if (newViews.includes("Video Feed") && newViews.length < 2) {
        this.viewOrientation = "webcam-full";
      }
      if (newViews.length > 1) {
        this.viewOrientation = "shared-left";
      }
      if (!newViews.length) {
        this.viewOrientation = "";
      }
    },
    viewOrientation(newView) {
      //adds padding as needed when different orientations are selected
      let type = newView.split("-");
      this.type = type[0];
      if (type[0] == "webcam") {
        if (type[1] == "80") {
          this.parentClass = "p-16";
        }
        if (type[1] == "60") {
          this.parentClass = "p-24";
        }
        if (type[1] == "full") {
          this.parentClass = "";
        }
      } else if (type[0] == "shared") {
        this.parentClass = "py-5";
      } else {
        this.parentClass = "";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@mixin image-template($name) {
  @apply w-full h-full relative;
  background-image: url("../assets/#{$name}.png");
  background-size: cover;
  background-repeat: no-repeat;
}

@mixin inner-template() {
  @include image-template("webcam-image");
  @apply absolute flex justify-center items-center w-1/4 h-1/4 bottom-0;
}

.stream-canvas {
  @apply w-full my-10 mx-20 flex flex-col justify-center items-center;

  .container {
    @apply bg-black max-h-full w-full flex items-center justify-center;
    aspect-ratio: 16/9;
    max-width: 1500px;
    margin-top: -60px;
  }
  .screenshare {
    @include image-template("screenshare-image");
  }
  .webcam-full {
    @include image-template("webcam-image");
  }
  .webcam-80 {
    @include image-template("webcam-image");
    background-size: auto;
  }
  .webcam-60 {
    @include image-template("webcam-image");
  }
  .shared-left {
    @include image-template("screenshare-image");
    .inner {
      @include inner-template();
      @apply left-4;
    }
  }
  .shared-right {
    @include image-template("screenshare-image");
    .inner {
      @include inner-template();
      @apply right-4;
    }
  }
  .shared-side {
    @include image-template("screenshare-image");
    background-size: 66% 100%;
    .inner {
      @include inner-template();
      @apply right-0 h-full w-1/3 bottom-0 bg-center;
    }
  }
}
</style>