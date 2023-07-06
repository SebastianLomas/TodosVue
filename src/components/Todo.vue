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


<style scoped>
.todo {
  display: flex;
  width: 50%;
  height: 2.5rem;
  background-color: #a4f1ad;
  align-items: center;
  padding: 0 0.5rem;
  border-left: 1rem solid #78d984;
  margin-bottom: 0.3rem;
}

.todo span {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1rem;
  text-transform: capitalize;
  user-select: none;
  color: #353131;
}
</style>