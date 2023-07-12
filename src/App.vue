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
        deleteTodo(event,todoId) {
          document.getElementById(todoId).classList.add("deleting")
          setTimeout(() => {
            this.todoList = this.todoList.filter(todo => todo.id !== todoId)
            this.saveHistorial(this.todoList)
            console.log(this.todoList)
          },500)
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
    <li class="todo" v-for="todo in todoList" :id="todo.id">
      <span>
        {{ todo.value }}
        <div class="round-button" @click="deleteTodo($event,todo.id)">
          <v-icon name="bi-trash-fill" />
        </div>
      </span>
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

.deleting {
  animation: deletingAnim 500ms cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
}

@keyframes deletingAnim {
  0% {
    transform: scale(1);
  }
  30% {
    transform: scale(0.9);
  }
  31% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-10rem);
    
  }
}

</style>