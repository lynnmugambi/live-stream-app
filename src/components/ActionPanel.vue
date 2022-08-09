<template>
  <!-- Action panel in the StreamCanvas component. Currently static-->
  <div class="action-panel">
    <ButtonComponent text="Chat"></ButtonComponent>
    <ButtonComponent text="Record"></ButtonComponent>
    <ButtonComponent text="Go Live" btnState="active"></ButtonComponent>
  </div>
</template>

<script>
import ButtonComponent from "./ButtonComponent.vue";
export default {
  components: { ButtonComponent },
};
</script>

<style lang="scss" scoped>
.action-panel {
  @apply inline-flex p-3 gap-2 border-slate-300 border-solid border-2 absolute bottom-0 max-w-2xl;
  border-top-right-radius: 15px;
  border-top-left-radius: 15px;
  width: 40%;

  .button {
    @apply grow;
  }
}
</style>