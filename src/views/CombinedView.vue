<template>
    <div>
        <h1>Lista Combinadas de Tareas</h1>
        <div class="add-task-container">
        <div class="input-group">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Añadir nueva tarea" 
                class="task-input"
                />
            <button @click="addTask" class="add-button">Añadir</button>
        </div>
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
    </div>
    </div>
        <!-- Esta seccion es una combinación de las dos vistas anteriores -->
</template>

<script>
  import axios from 'axios';
export default {
    name: "CombinedView",
    data() {
        return {
            newtask: "", 
            tasks: [], 
        };
    },
    created() {
        this.fetchTasks();
    },
    methods: {
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
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(), 
            }; 
            this.tasks.push(newTask);
            this.tasks.unshift(newTask);
            this.newTask = ""; 
        },
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
            
        },
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
   },
};
   // Esta sección debe permitir agregar tareas nuevas a la vez que extraer las tareas anteriores de la API
</script>

<style scoped>
.add-task-container {
    padding: 20px;
    max-width: 600px;
    margin: 0 auto;
}

.input-group {
    display: flex;
    margin-bottom: 10px;
}

.task-input {
    flex-grow: 1;
    padding: 8px;
    margin-right: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.add-button {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
}

.task-list {
    margin-top: 20px;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #eee;
}

.completed {
    text-decoration: line-through;
    color: gray;
}
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