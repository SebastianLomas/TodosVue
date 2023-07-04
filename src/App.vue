<script>
  import { ref } from 'vue';

  export default {
    data() {
      return {
        count: 0,
        todoList: []
      }
    },

    methods: {
      increment() {
        this.count++
      },
      addTodo() {
        if(document.querySelector('.input-text').value.length > 0) {
          this.todoList.push(document.querySelector('.input-text').value)
          document.querySelector('.input-text').value = ""
          localStorage.setItem("historial", JSON.stringify(this.todoList))
        }
      },
      loadHistorial()  {
        const historial = localStorage.getItem("historial")
        if(historial) {
          this.todoList.push(...JSON.parse(historial))
        }
      }
    },

    mounted() {
      this.loadHistorial()
      this.increment()
    }
  }

</script>

<template>
  <div class="input-wrapper">
    <input class="input-text" type="text" placeholder="Agrega un Tarea"/>
    <button class="input-button" @click="addTodo()">Agregar Tarea</button>
  </div>
  <ul class="todo-wrapper">
    <li class="todo" v-for="todo in todoList">
      <span>{{ todo }}</span>
    </li>
  </ul>
</template>

<style scoped>
.input-wrapper {
  width: 100%;
  height: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.input-text {
  display: block;
  width: 30rem;
  height: 4rem;
  font-size: 1rem;
  padding: 0 0.9rem;
  margin-right: 0.5rem;
  outline: none;
}

.input-text:focus {
  background-color: rgb(235, 235, 235);
  border-bottom: 0.2rem solid #719eed;
  transition: 100ms;
}

.input-button {
  width: 10rem;
  height: 4rem;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  font-size: 1rem;
  background-color: #719eed;
}

.input-button:hover {
  transform: scale(0.99);
  transform: translateY(0.1rem);
  background-color: #638ace;
  transition: 100ms;
}

.todo-wrapper {
  width: 100%;
  min-height: 6rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

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
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1rem;
  text-transform: capitalize;
}
</style>