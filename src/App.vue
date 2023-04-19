<template>

  <div class="todo-list">
    <h1>LIST KEGIATAN</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Tambahkan Kegiatan Baru Anda">
      <button>Tambah</button>
    </form>
    <div class="filter-buttons">
      <button @click="filter = 'all'">Semua</button>
      <button @click="filter = 'active'">Sedang Dikerjakan</button>
      <button @click="filter = 'completed'">Selesai</button>
    </div>
    <ul>
      <li v-for="(todo, index) in filteredTodos" :key="index" :class="{ completed: todo.completed }">
        <input type="checkbox" v-model="todo.completed" @change="updateTodo" />
        <span>{{ todo.text }}</span>
        <div class="buttons">
          <button @click="removeTodo(index)">Hapus Tugas</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { text: 'Kasih Makan Kucing', completed: false },
        { text: 'Farming Item Ayaka', completed: false },
        { text: 'Exploring Inazuma', completed: false }
      ],
      newTodo: '',
      filter: 'all'
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo) {
        this.todos.push({
          text: this.newTodo,
          completed: false
        })
        this.newTodo = ''
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    completeTodo(index) {
      this.todos[index].completed = true
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'completed') {
        return this.todos.filter(todo => todo.completed)
      } else if (this.filter === 'active') {
        return this.todos.filter(todo => !todo.completed)
      } else {
        return this.todos
      }
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500&family=Roboto:wght@300;500&display=swap');
*{
  font-family: roboto;
}
h1{
  font-weight: bolder;
}
body{
  background-color: #FFF3E2;
}
.todo-list {
  margin: 20px auto;
  max-width: 600px;
  text-align: center;
}

form {
  margin: 20px 0;
  display: flex;
  justify-content: space-between;

}

input[type="text"] {
  padding: 10px;
  border: none;
  border-radius: 5px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
  margin-right: 10px;
  width: 80%;
  background-color: #FA9884;
  color: black ;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #E74646;
  color: #FFF3E2;
  cursor: pointer;
  margin: 0 5px;
}
button:hover{
  background-color:#D21312;
}
button:active{
  background-color: #CE5959;
}
::placeholder{
  color:black;
  opacity: 0.5;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #FA9884;
  margin-bottom: 10px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  font-size:large;
}

.completed {
  text-decoration: line-through;
}

.filter-buttons {
  margin-bottom: 20px;
}

input[type='checkbox']{
  content: "";
  display: flex;
  width: 25px;
  height: 25px;
  border: 2px solid #555555;
  border-radius: 3px;
  background-color: black;
}

</style>
