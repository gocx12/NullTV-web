<template>
  <v-footer
    app
    class="d-flex justify-center">
    <div>
      <v-btn
        v-for="icon in icons"
        :key="icon"
        class="mx-4"
        :icon="icon"
        variant="text"
      ></v-btn>
    </div>
    <span class="white--text">&copy; {{ new Date().getFullYear() }}</span>
  </v-footer>
</template>

<script setup>
  const icons = [
    'mdi-github',
  ]
</script>