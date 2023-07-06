<script>

import RoundButton from "./RoundButton.vue"

export default {
  props: {
    todoText: String
  },
  components: {RoundButton}
}

</script>

<template>
  <li class="todo">
    <span>
      {{ todoText }}
      <RoundButton />
    </span>
  </li>
</template>
