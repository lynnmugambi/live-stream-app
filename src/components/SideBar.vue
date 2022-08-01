<template>
  <div class="side-bar">
    <div class="content">
      <ButtonComponent
        text="Add Source"
        btnState="active"
        @btnClicked="openModal"
      ></ButtonComponent>
      <div v-if="!hasSource" class="source-placeholder">
        <span class="plus"> + </span>
        <span class="text-black text-lg font-bold">Add Media Source</span>
        <span class="text-small">Screenshare, Camera</span>
      </div>
    </div>
  </div>
</template>

<script>
import ButtonComponent from "./ButtonComponent.vue";

export default {
  name: "SideBar",
  components: { ButtonComponent },
  data() {
    return {
      sourceList: [],
    };
  },
  computed: {
    hasSource() {
      return this.sourceList.length > 1;
    },
  },
  methods: {
    openModal() {
      console.log("modal opened");
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