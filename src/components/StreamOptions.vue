<template>
  <div class="stream-options pt-6">
    <div class="webcam inline-flex flex-row gap-4" v-if="showCamOnly">
      <div
        class="opt-container"
        @click="selectView('selectedCam', 'webcam-full')"
        :class="[selectedCam == 'webcam-full' ? 'selected' : '']"
      >
        <div class="inner inner-full">
          <UserIcon viewBox="0 0 36 37" />
        </div>
      </div>
      <div
        class="opt-container inner-80"
        @click="selectView('selectedCam', 'webcam-80')"
        :class="[selectedCam == 'webcam-80' ? 'selected' : '']"
      >
        <div class="inner">
          <UserIcon viewBox="0 0 36 37" />
        </div>
      </div>
      <div
        class="opt-container inner-60"
        @click="selectView('selectedCam', 'webcam-60')"
        :class="[selectedCam == 'webcam-60' ? 'selected' : '']"
      >
        <div class="inner">
          <UserIcon viewBox="0 0 36 37" />
        </div>
      </div>
    </div>
    <div class="screenshare" v-if="showScreenOnly">
      <div class="opt-container">
        <ScreenshareIcon viewBox="0 0 36 36" />
      </div>
    </div>
    <div
      class="webcam-screenshare inline-flex flex-row gap-4"
      v-if="showCamAndScreen"
    >
      <div
        class="opt-container"
        @click="selectView('selectedWebAndCam', 'shared-left')"
        :class="[selectedWebAndCam == 'shared-left' ? 'selected' : '']"
      >
        <ScreenshareIcon viewBox="0 0 36 36" />
        <div class="inner inner-left">
          <UserIcon viewBox="0 0 36 37" />
        </div>
      </div>
      <div
        class="opt-container"
        @click="selectView('selectedWebAndCam', 'shared-right')"
        :class="[selectedWebAndCam == 'shared-right' ? 'selected' : '']"
      >
        <ScreenshareIcon viewBox="0 0 36 36" />
        <div class="inner inner-right">
          <UserIcon viewBox="0 0 36 37" />
        </div>
      </div>
      <div
        class="opt-container"
        @click="selectView('selectedWebAndCam', 'shared-side')"
        :class="[selectedWebAndCam == 'shared-side' ? 'selected' : '']"
      >
        <ScreenshareIcon class="mr-8" viewBox="0 0 36 36" />
        <div class="inner side">
          <UserIcon viewBox="0 0 36 37" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserIcon from "@/assets/user-icon.svg";
import ScreenshareIcon from "@/assets/screenshare-icon.svg";
export default {
  name: "StreamOptions",
  components: {
    UserIcon,
    ScreenshareIcon,
  },
  props: {
    views: {
      type: Array,
      default: () => [],
    },
  },
  watch: {
    views(newValue) {
      if (newValue) {
        this.selectedCam = "webcam-full";
        this.selectedWebAndCam = "shared-left";
      }
    },
  },
  data() {
    return {
      selectedCam: "webcam-full",
      selectedWebAndCam: "shared-left",
    };
  },
  computed: {
    showCamOnly() {
      return this.views.includes("Video Feed") && this.views.length < 2;
    },
    showScreenOnly() {
      return this.views.includes("Screenshare") && this.views.length < 2;
    },
    showCamAndScreen() {
      return this.views.length > 1;
    },
  },
  methods: {
    selectView(type, orientation) {
      this[type] = orientation;
      this.$emit("orientViews", orientation);
    },
  },
};
</script>

<style lang="scss" scoped>
$greyIconColor: #91979a;

.stream-options {
  .webcam {
    .opt-container {
      @apply w-28 h-20 rounded-xl flex justify-center items-center;
      background: var(--lightGreyBg);

      .inner {
        @apply rounded-lg w-full h-full flex justify-center items-center;
        background: var(--darkGreyBg);

        svg {
          color: $greyIconColor;
          width: 24px;
        }
      }
      .inner-full {
        @apply rounded-xl;
        background: var(--lightGreyBg) !important;
      }
    }
    .selected {
      border: 4px solid var(--darkTeal);
      background: white;

      .inner {
        background: var(--lightTeal);

        svg {
          color: var(--darkTeal);
        }
      }
    }
    .inner-80 {
      @apply p-3;
    }
    .inner-60 {
      @apply p-4;
    }
  }
  .screenshare {
    .opt-container {
      @apply w-28 h-20 rounded-xl flex justify-center items-center;
      background: var(--lightTeal);
      svg {
        color: var(--darkTeal);
        width: 24px;
      }
    }
  }
  .webcam-screenshare {
    .opt-container {
      @apply w-28 h-20 rounded-xl flex justify-center items-center relative;
      background: var(--lightGreyBg);
      svg {
        color: $greyIconColor;
        width: 24px;
      }
      .inner-left {
        @apply left-2;
        svg {
          width: 12px;
        }
      }
      .inner-right {
        @apply right-2;
        svg {
          width: 12px;
        }
      }
      .inner {
        @apply rounded-lg absolute flex justify-center items-center bottom-2 w-7 h-6;
        background: var(--darkGreyBg);
      }
      .side {
        @apply right-0 h-full w-1/3 bottom-0;
        border-top-left-radius: 0;
        border-bottom-left-radius: 0;
        svg {
          width: 22px;
        }
      }
    }
    .selected {
      border: 4px solid var(--darkTeal);
      background: var(--lightTeal);
      svg {
        color: var(--darkTeal);
      }

      .inner {
        background: white;
        svg {
          color: var(--darkTeal);
        }
      }
    }
  }
}
</style>