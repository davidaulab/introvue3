<template>
  <h1>Aplicación ToDo-List</h1>

  <form @submit.prevent="addTodo()">
    <label>Nueva tarea:</label>
    <input v-model="newTodo" name="newTodo" autocomplete="off">
    <button>Añadir</button>
  </form>
  <h2>Lista de Tareas</h2>
  <ul>
    <li v-for="(todo, index) in data" :key="index">
        <span :class="{ done: todo.done}" @click="doneTodo(todo)">{{ todo.description }}</span>&nbsp;
        <button @click="removeTodo (index)"> - </button>
    </li>
  </ul>

</template>

<script>
import { ref } from 'vue';
export default {
  name: 'Aplicación ToDo-List en VUE',
  
  setup (){
    const data = ref ([{
      done: false,
      description: 'Primera tarea',
    },
    {
      done: true,
      description: 'Segunda tarea',
    }
    ]);
    const newTodo = ref ('');


    function addTodo () {
      //alert ('new Todo');
      if (newTodo.value){
        data.value.push ({
          done: false,
          description: newTodo.value,
        });
        newTodo.value = '';
      }

    }
    function doneTodo(todo) {
        todo.done = !todo.done;
        /*
        if (!todo.done)
          todo.done = true;
        else 
          todo.done = false;*/
    }

    function removeTodo (index) {
   
      if (confirm ('Estás seguro de eliminar la tarea')) {
       data.value.splice (index, 1);
      }
     
    }

    return {
      data,
      newTodo,
      addTodo,
      doneTodo,
      removeTodo,
      
    }
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
  color: green;
}
</style>
