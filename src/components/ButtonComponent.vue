<template>
  <div class="button" :class="getClass" @click="emitClick">{{ text }}</div>
</template>

<script>
export default {
  name: "ButtonComponent",
  props: {
    text: {
      type: String,
      default: "Add Text",
      required: true,
    },
    btnState: {
      type: String,
    },
  },
  computed: {
    getClass() {
      return this.btnState ? `button-${this.btnState}` : "";
    },
  },
  methods: {
    emitClick() {
      this.$emit("btnClicked");
    },
  },
};
</script>

<style lang="scss" scoped>
.button {
  @apply py-2 px-4 rounded text-black flex justify-center items-center;
  font-weight: 700;
  background-color: var(--lightGreyBtn);

  &[disabled] {
    background-color: var(--darkGreyBg);
  }

  &-active {
    @apply text-white;
    background-color: var(--darkTeal);
  }

  &-hide {
    @apply bg-white;
    color: var(--redText);
  }
}
</style>