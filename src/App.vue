<template v-if="">
  <div class="main-wrapper">
    <button id="open-modal-button" @click="isOpen = true" class="open-modal-button"></button>
    <modal :open="isOpen" @close="isOpen = !isOpen">
    </modal>
  </div>

</template>

<script>
import { ref } from "vue"
import Modal from "./components/Modal-block.vue"
export default {
  name: 'App',
  components: {
    Modal
  },
  setup () {
    const isOpen = ref(false)
    return { isOpen }
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  margin: 0;
}
#app .main-wrapper {
  background-image: url("/src/assets/bg.png");
  background-repeat: no-repeat;
  background-position: center;
  height: 52.5em;
  width: 90em;
}
.open-modal-button {
  top: 573px;
  left: 68em;
  width: 271px;
  height: 48px;
  cursor: pointer;
  opacity: 0;
  position: absolute;
}
.invite-others--header {
  width: 514px;
  height: 32px;
  font-family: 'Open Sans';
  font-style: normal;
  font-weight: 600;
  font-size: 27px;
  line-height: 44px;
  font-feature-settings: 'ss01' on;
  color: #3C1F1D;
  flex: none;
  order: 0;
  flex-grow: 1;
}
</style>
