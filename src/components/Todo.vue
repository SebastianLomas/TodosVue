<script setup>
  defineProps({
    todoText: String
  })
</script>

<template>
  <li class="todo">
    <span>{{ todoText }}</span>
  </li>
</template>