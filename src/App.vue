<script>
  import RoundButton from './components/RoundButton.vue';
  import Todo from './components/Todo.vue';

/*   const deleteTodo = function(ev) {
    console.log(ev)
  } */
  export default {
    data() {
        return {
            count: 0,
            todoList: []
        };
    },
    methods: {
        increment() {
            this.count++;
        },
        addTodo() {
            if (document.querySelector(".input-text").value.length > 0) {
                this.todoList.push({id: this.count, value: document.querySelector(".input-text").value});
                this.increment()
                document.querySelector(".input-text").value = "";
                this.saveHistorial(this.todoList)
            }
        },
        getUnusedId() {
          const todoListLen = this.todoList.length
          return todoListLen
        },
        saveHistorial(finalTodoList) {
          localStorage.setItem("historial", JSON.stringify(finalTodoList));
        }
        ,
        loadHistorial() {
            const historial = localStorage.getItem("historial");
            if (historial) {
                this.todoList.push(...JSON.parse(historial));
                this.count = this.getUnusedId()
            }
        },
        deleteTodo(ev) {
          const todoId = ev.target.id || ev.target.parentElement.id || ev.target.parentElement.parentNode.id
          this.todoList = this.todoList.filter(todo => todo.id != todoId)
          this.saveHistorial(this.todoList)
          console.log(this.todoList)
          console.log(ev)
          console.log(ev.target.parentElement.parentNode.id)
          console.log(ev.target.id || ev.target.parentElement.id || ev.target.parentElement.parentNode.id)
        }
    },
    mounted() {
        this.loadHistorial();
    },
    components: { RoundButton, Todo }
}

</script>

<template>
  <div class="input-wrapper">
    <input class="input-text" type="text" placeholder="Agrega un Tarea"/>
    <button class="input-button" @click="addTodo()">Agregar Tarea</button>
  </div>
  <ul class="todo-wrapper">
    <Todo v-for="todo in todoList" :todoText="todo.value" />
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
  border-bottom: 0.2rem solid #3b3b3b0c;
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


</style>