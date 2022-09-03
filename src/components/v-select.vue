<template>
  <div class="v-select">
    <div class="options">
      <div>
        <h4
          :v-for = "guest"
        >Guest</h4>
        <p>Guest text</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-select"
}
</script>

<style scoped>

</style>