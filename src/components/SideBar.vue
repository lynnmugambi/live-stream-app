<template>
  <div class="side-bar">
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
      <div v-else></div>
    </div>
    <ModalComponent
      v-if="showModal"
      @close="showModal = false"
      @addSource="showSource($event)"
    ></ModalComponent>
  </div>
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
    };
  },
  methods: {
    openModal() {
      this.showModal = true;
      console.log("modal opened");
    },
    showSource(value) {
      this.sourceList = value;
    },
  },
};
</script>

<style lang="scss" scoped>
.side-bar {
  @apply flex flex-col h-full border-r-slate-300 border-solid border-r-2 w-1/4;
  min-width: 200px;

  .content {
    @apply p-4 w-full h-full inline-flex gap-2 flex-col;

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