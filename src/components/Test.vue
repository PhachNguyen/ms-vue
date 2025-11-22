<template>
  <div>
    <h3>{{ user.name }}</h3>
    <p>Tuổi: {{ user.age }}</p>
  </div>
</template>

<script setup>
const props = defineProps({
  user: Object,
})
</script>
