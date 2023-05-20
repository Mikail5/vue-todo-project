<template>
  <div class="container">
    <header class="mb-4">
      <h2 class="m-0">TODO List</h2>
      <input
        type="text"
        class="form-control"
        v-model="todoInput"
        @keyup.enter="insertaTarea"
        v-on:blur="insertaTarea"
      >
    </header>
    <main>
      <ul class="list-group">
        <li class="list-group-item" v-for="(todo) in todos" :key="todo.id">
          <div class="row align-items-center">
            <div class="col">
              <div v-if="todo.isUpdate">
                <input
                  type="text"
                  class="form-control"
                  v-model="todo.titulo"
                  @keyup.enter="actualizarTarea(todo)"
                  v-on:blur="actualizarTarea(todo)"
                >
              </div>
              <div v-else>
                <div class="custom-control custom-checkbox">
                  <input
                    type="checkbox"
                    :id="`checkbox${todo.id}`"
                    class="custom-control-input"
                    v-model="todo.completado"
                  >
                  <label class="custom-control-label" :for="`checkbox${todo.id}`">
                    <span>{{todo.titulo}}</span>
                  </label>
                </div>
              </div>
            </div>
            <div class="col-auto">
              <button class="btn btn-warning mr-2" @click="abrirActualizar(todo.id)">Actualizar</button>
              <button class="btn btn-danger" @click="eliminarTarea(todo.id)">Eliminar</button>
            </div>
          </div>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>export default {
  name: 'TodoManager',
  data: function (){
    return {
      todoInput:'',
      todoInputUpdate:'',
      todos: [
        {
          id: 0,
          titulo: 'Hacer las compras',
          completado: false,
          isUpdate: false
        },
        {
          id: 1,
          titulo: 'Pasear al perro',
          completado: true,
          isUpdate: false
        },
        {
          id: 2,
          titulo: 'Salir a trotar',
          completado: false,
          isUpdate: false
        }
      ]
    }
  },
  props: {
    msg: String
  },
  methods:{
    insertaTarea(evento){
      console.log(evento);
      if(this.validarCampoVacio(this.todoInput)) return;

      let length = this.todos.length - 1;
      let lastData = this.todos[length] || { id: 0 };
      let id = lastData.id + 1;
      let todoNuevo = {
        id: id,
        titulo: this.todoInput,
        completado: false
      }
      this.todos.push(todoNuevo);
      this.todoInput='';
    },
    eliminarTarea(id){
      let todoRestantes=this.todos.filter(todo => todo.id !== id)
      this.todos=todoRestantes;
    },
    actualizarTarea(todo){
      if(this.validarCampoVacio(todo.titulo))
        return;
      let todoRestantes = this.todos.map(t => ( 
          t.id !== todo.id ? t : { ...t, isUpdate: false }
      ));
      this.todos=todoRestantes;
      this.todoInputUpdate='';
    },
    abrirActualizar(id){
       let todoRestantes=this.todos.map(todo => ( 
          todo.id !== id ? todo : { ...todo, isUpdate: true }
      ));
      this.todos=todoRestantes;
    },
    validarCampoVacio(titulo){
      if(titulo.trim() === ""){
        alert('El campo ha actualizar no debe estar vacio');
        return true;
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>