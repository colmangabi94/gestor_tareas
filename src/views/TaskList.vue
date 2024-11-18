<template>
    <div>
        <h1>Lista de Tareas</h1>
        <button @click="fetchTasks">Cargar Tareas</button>
        <div v-if="tasks.length > 0">
            <div v-for="task in tasks" :key="task.id">
                <div>
                    <h5 :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.todo }}</h5>
                    <span>{{ task.completed ? 'Completada' : 'Pendiente' }}</span>
                    <button @click="toggleTaskCompletion(task)">
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button @click="deleteTask(task)">Eliminar</button>
                </div>
            </div>
        </div>
        <div v-else>
<p>No hay tareas disponibles. Haz clic en "Cargar Tareas"</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: "TaskList",
    data() {
        return {
            tasks: [], // Almacenamiento local de las tareas traídas de la API
        };
    },
    methods: {
        // Llamada para obtener las tareas desde la API externa
        fetchTasks() {
            axios 
                .get('https://dummyjson.com/todos') // URL de la API
                .then((response) => {
                    this.tasks = response.data.todos; 
                })
                .catch((error) => {
                    console.log(error);
                });
        }, 
        // Cambiar el estado de una tarea (completada/no completada)
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Eliminar la tarea seleccionada
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
}; 
</script>

<style scoped>
/* Estilos básicos */
h1 {
    font-size: 24px;
    margin-bottom: 20px;
}

button {
    margin-left: 10px;
    padding: 5px 10px;
    cursor: pointer;
    border: none;
    background-color: #007bff;
    color: white;
    border-radius: 5px;
    font-size: 14px;
}

button:hover {
    background-color: #0056b3;
}

h5 {
    display: inline-block;
    margin-right: 10px;
}

div {
    margin-bottom: 15px;
}

p {
    font-style: italic;
    color: #888;
}
</style>