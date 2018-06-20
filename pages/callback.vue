<template>
  <div class="container d-flex align-items-center justify-content-center flex-column">
    <v-progress-circular :size="70" :width="7" indeterminate color="green"></v-progress-circular>
    Logging in...
  </div>
</template>

<style scoped>
.container {
  min-height: 70vh;
}
</style>
