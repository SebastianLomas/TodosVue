<script>

</script>

<template>
  <div class="round-button">
    <v-icon name="bi-trash-fill" />
  </div>
</template>

<style scoped>
  .round-button {
    width: 2rem;
    height: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    /* border: 1px solid #7bc784; */
    color: #353131;
    border-radius: 100%;
    background-color: #95e19e;
  }

  .round-button:hover {
    color: rgb(235, 229, 229);
    transform: rotate(-30deg);
    cursor: pointer;
    background-color: #5ca064;
    transition: 100ms;
  }

  .round-button:active {
    background-color: #3e7044;
    transition: 100ms;
  }
</style>