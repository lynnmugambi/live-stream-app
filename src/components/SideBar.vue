<template>
  <aside class="side-bar">
    <div class="content">
      <ButtonComponent
        text="Add Source"
        btnState="active"
        @btnClicked="openModal"
      ></ButtonComponent>
      <div v-if="!sourceList.length" class="source-placeholder">
        <span class="plus"> + </span>
        <span class="text-black text-lg font-bold">Add Media Source</span>
        <span class="text-small">Screenshare, Camera</span>
      </div>
      <div v-else class="inline-flex gap-2 flex-col">
        <div
          v-for="(source, index) in sourceList"
          :key="index"
          class="source-container"
          :class="source.class"
          @click="toggleStream(source.name)"
        >
          <ButtonComponent
            :text="btnText(source.name)"
            :btnState="btnState(source.name)"
          ></ButtonComponent>
          <span>{{ source.text }}</span>
        </div>
      </div>
    </div>
    <ModalComponent
      v-if="showModal"
      @close="showModal = false"
      @addSource="showSource($event)"
    ></ModalComponent>
  </aside>
</template>

<script>
import ButtonComponent from "./ButtonComponent.vue";
import ModalComponent from "./ModalComponent.vue";

export default {
  name: "SideBar",
  components: { ButtonComponent, ModalComponent },
  data() {
    return {
      sourceList: [],
      showModal: false,
      inStream: [],
    };
  },
  computed: {
    btnText() {
      return (source) =>
        this.inStream.includes(source) ? "hide on stream" : "show on stream";
    },
    btnState() {
      return (source) => (this.inStream.includes(source) ? "hide" : "active");
    },
  },
  watch: {
    sourceList(newValue) {
      if (newValue) {
        // clear current view if sourceList changes, helps remove stale state.
        this.inStream = [];
        this.$emit("views", this.inStream);
      }
    },
  },
  methods: {
    openModal() {
      this.showModal = true;
    },
    showSource(value) {
      let sources = [];
      value.forEach((element) => {
        sources.push({
          name: element,
          class: element === "Screenshare" ? "screenshare" : "webcam",
          text: element === "Screenshare" ? "My screen feed " : "My video feed",
        });
      });
      this.sourceList = sources;
    },
    toggleStream(source) {
      if (this.inStream.includes(source)) {
        //remove source if exists in array
        let index = this.inStream.findIndex((e) => e == source);
        this.inStream.splice(index, 1);
      } else {
        //add source to array
        this.inStream.push(source);
      }
      //emit to parent component
      this.$emit("views", this.inStream);
    },
  },
};
</script>

<style lang="scss" scoped>
@mixin image-template($name) {
  background-image: url("../assets/#{$name}.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.side-bar {
  @apply flex flex-col h-full border-r-slate-300 border-solid border-r-2 w-1/4;
  min-width: 200px;
  max-width: 300px;

  .content {
    @apply p-4 w-full h-full inline-flex gap-2 flex-col;

    .source-container {
      @apply flex flex-col justify-center items-center rounded h-28 relative;

      .button {
        @apply font-normal p-2 text-xs;
      }

      span {
        @apply absolute text-xs text-left left-1 bottom-1 text-white;
      }
    }

    .screenshare {
      @include image-template("screenshare-image");
    }
    .webcam {
      @include image-template("webcam-image");
    }

    .source-placeholder {
      @apply flex flex-col justify-center items-center p-6 rounded text-center;
      background-color: var(--lightGreyBtn);

      .plus {
        @apply text-5xl pt-2;
        color: var(--darkTeal);
      }
      .text-small {
        @apply text-sm;
        color: var(--greyText);
      }
    }
  }
}
</style>