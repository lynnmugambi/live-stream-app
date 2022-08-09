<template>
  <!-- Modal component used to select sources for the side panel-->
  <div
    class="modal"
    aria-labelledby="modal-title"
    role="dialog"
    aria-modal="true"
  >
    <div class="modal-background">
      <div class="modal-container">
        <div class="modal-content">
          <div class="modal-header">
            <h3 class="modal-header__text">Add a new media source</h3>
            <!--Close Icon to exit modal-->
            <button
              type="button"
              class="modal-header__button"
              @click="closeModalIcon"
            >
              <svg
                aria-hidden="true"
                class="w-5 h-5"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                  clip-rule="evenodd"
                ></path>
              </svg>
              <span class="sr-only">Close modal</span>
            </button>
          </div>
          <div class="modal-body">
            <!-- Reusable component to display the different sources available -->
            <div
              v-for="(source, index) in sources"
              :key="index"
              class="box"
              @click="addSource(source.title)"
              :class="{ selected: selectedSources.includes(source.title) }"
            >
              <h4 class="box-title">{{ source.title }}</h4>
              <p class="box-text">{{ source.text }}</p>
            </div>
          </div>
          <div class="flex justify-end p-4 rounded-b border-t border-gray-200">
            <!-- Button component to submit selected sources-->
            <ButtonComponent
              text="Submit"
              btnState="active"
              :disabled="!selectedSources.length"
              @btnClicked="closeModal"
            ></ButtonComponent>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ButtonComponent from "./ButtonComponent.vue";
export default {
  name: "ModalComponent",

  data() {
    return {
      sources: [
        {
          title: "Screenshare",
          text: "Share your entire screen, window or a specific Chrome tab",
        },
        {
          title: "Video Feed",
          text: "Share a feed of your in-built webcam and microphone. If you do not have a webcam, you can use a “virtual” webcam such as Streamlabs Desktop virtual camera",
        },
      ],
      selectedSources: [],
    };
  },
  methods: {
    closeModalIcon() {
      this.$emit("close");
    },
    closeModal() {
      this.$emit("addSource", this.selectedSources);
      this.$emit("close");
    },
    addSource(source) {
      if (this.selectedSources.includes(source)) {
        //removes source if already exixts in selectedSources array
        let index = this.selectedSources.findIndex((e) => e == source);
        this.selectedSources.splice(index, 1);
      } else {
        this.selectedSources.push(source);
      }
    },
  },
  components: { ButtonComponent },
};
</script>

<style lang="scss" scoped>
.modal {
  @apply relative z-10;

  &-background {
    @apply overflow-y-auto overflow-x-hidden fixed w-full z-20 inset-0 bg-gray-500 bg-opacity-75 flex justify-center items-center;
  }
  &-container {
    @apply p-4;

    .modal-content {
      @apply bg-white rounded-lg shadow;

      .modal-header {
        @apply flex justify-center items-start p-4 rounded relative;

        &__text {
          @apply text-xl font-semibold text-black text-center;
        }

        &__button {
          @apply text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto absolute top-4 right-4;
        }
      }
      .modal-body {
        @apply px-10 pb-10 pt-4 inline-flex flex-row gap-8;

        .box {
          @apply flex justify-start flex-col items-center w-60 h-60;
          background-color: var(--lightGreyBtn);

          &-title {
            @apply text-lg text-black font-semibold pt-10;
          }

          &-text {
            @apply p-4 text-sm text-center;
            color: var(--greyText);
          }
        }
        .selected {
          @apply rounded;
          border: 4px solid var(--darkTeal);
        }
      }
    }
  }
}
</style>