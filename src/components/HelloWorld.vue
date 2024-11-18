<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Esta aplicación te permite gestionar tus tareas de manera eficiente. Puedes añadir nuevas tareas manualmente o extraerlas desde una API.
    </p>
    <h3>Secciones</h3>
    <h5>Añadir tarea</h5>
    <p>Permite ingresar nuevas tareas manualmente.</p>
    <h5>Lista de tareas</h5>
    <p>Muestra todas las tareas extraídas desde la API, permitiendo marcarlas como completadas o eliminarlas.</p>
    <h5>Listas combinadas</h5>
    <p>Combina las funcionalidades de añadir tareas manualmente y ver las tareas de la API al mismo tiempo.</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
