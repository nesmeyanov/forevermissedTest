<template v-if="">
  <div class="main-wrapper">
    <button id="open-modal-button" @click="isOpen = true" class="open-modal-button"></button>
    <modal :open="isOpen" @close="isOpen = !isOpen">
    </modal>
  </div>

</template>

<script>
import { ref } from "vue"
import Modal from "./components/modal-block.vue"
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

<style>

#app {
  font-family: 'openSansRegular';
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
  left: 71.4em;
  width: 272px;
  height: 48px;
  cursor: pointer;
  opacity: 0;
  position: absolute;
}
.invite-others--header {
  width: 514px;
  height: 31px;
  font-family: 'Open Sans';
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 44px;
  color: #3C1F1D;
}
</style>
