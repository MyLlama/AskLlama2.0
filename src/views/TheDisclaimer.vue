<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal" :style="modalStyles">
        <header class="modal-header">
          <slot name="header"></slot>
          <button type="button" class="btn-close" @click="close">×</button>
        </header>

        <section class="modal-body">
          <slot name="body"></slot>
        </section>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "TheDisclaimer",
  props: {
    modalWidth: String,
    modalHeight: String,
  },
  computed: {
    modalStyles() {
      return {
        width: this.modalWidth,
        height: this.modalHeight,
      };
    },
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.3);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  width: 50%;
  height: 56vh;
  z-index: 100;
  border: none;
  background: #ffffff;
  box-shadow: 0 2px 8px rgba(240, 120, 18, 0.3);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  border-radius: 30px;
  font-family: "Trebuchet MS", sans-serif;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  justify-content: center;
  text-align: center;
  font-size: 17px;
  color: black;
  background-color: #f07812;
}

.modal-body {
  position: relative;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  color: black;
  flex-grow: 1;
  overflow-x: hidden;
  text-align: left;
}

.btn-close {
  position: absolute;
  top: 0.5vw;
  right: 2vw;
  border: none;
  font-size: 2rem;
  height: 40px;
  width: 40px;
  cursor: pointer;
  font-weight: bold;
  color: black;
  background: transparent;
  border-radius: 50%;
}

.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}
.modal-fade-enter-active {
  animation: modal 0.5s ease-out;
}
.modal-fade-leave-active {
  animation: modal 0.5s ease-in reverse;
}
@keyframes modal {
  from {
    opacity: 0;
    transform: translateY(-50px) scale(0.9);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@media (max-width: 767px) {
  .modal {
    width: 80% !important;
    height: 47vh !important;
  }
  .btn-close {
    top: 2.1vw;
    right: 2vw;
  }
}
</style>
