<template>
  <div id="app">
    <div class="cabecalho">     
      <div>
        <h5>To Do List - Gerenciador de tarefas</h5>
      </div>   
    </div>

    <div class="container grid-xs py-2">
      <img class="img-responsive img-logo" src="@/assets/logo.png" alt="Logo tarefas">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input type="text" v-model="todo.description" class="form-input" placeholder="Nova tarefa">
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
      </form>
      
      <div class="todo-list">
        <todo v-for="t in todos" :key="t.id" @toggle="toggleTodo" @remove="removeTodo" :todo="t" />
      </div>
    </div>

    <div class="rodape">
      Projeto desenvolvido por Victória Lemos   
    </div>

  </div>
</template>

<script>
import Todo from './components/Todo'

export default {
  name: 'App',
  components: { Todo },
  data(){
    return { todos: [], todo: { checked: false } };
  },
  methods: {
    addTodo(todo){
      todo.id = Date.now();
      this.todos.push(todo);
      this.todo = { checked: false };
    },
    
    toggleTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if (index > -1){
        const checked = !this.todos[index].checked;
        this.$set(this.todos, index, { ...this.todos[index], checked });
      }
    },

    removeTodo(todo){
      const index = this.todos.findIndex(item => item.id === todo.id);
      if (index > -1){
        this.$delete(this.todos, index);
      }
    }
  }
};
</script>

<style scoped>

.img-logo{
  max-width: 100px;
  margin: 0 auto;
  padding-bottom: 1rem;
}

.todo-list{
  padding-top: 1.5rem;
}

.cabecalho {
  background: #5755d9;
  width: 100%;
  padding: 8px;
  margin-bottom: 20px;
}

h5{
  text-align: center;
  color: white;
  margin: 10px;
}

.rodape {
  background: #5755d9;
  color: white;
  width: 100%;
  bottom: 0px;
  text-align: center;
  position: fixed;
  padding-top: 16px;
  padding-bottom: 16px;
}
</style>