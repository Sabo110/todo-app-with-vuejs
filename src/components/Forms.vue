<template>
    <div class="flex flex-wrap justify-center gap-8 pt-4">
        <section class="w-96">
            <div class="mb-4 flex gap-4">
                <input type="email" id="email" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Enter your task"  v-model="taskObject.task" required />
                <Add @click="handleClick" />
            </div>
        </section>
        <section>
            <ShowTask :tasks="tasks" @deleteTask="handleDelete" @deleteAllTasks="handleDeleleAll"/>
        </section>
    </div>
</template>

<script setup>
import { reactive, ref } from "vue";
import Add from "./icons/Add.vue";
import ShowTask from "./ShowTask.vue";

const taskObject = ref({task: '', completed: false})
const tasks = ref([])
const handleClick = () => {
    tasks.value.push({...taskObject.value, id:tasks.value.length})
    taskObject.value.task = ''
}
const handleDelete = (id) => {
    let index = tasks.value.findIndex(task => task.id === id);
    tasks.value.splice(index, 1)
}
const handleDeleleAll = () => {
    tasks.value.length = 0
}
</script>

<style scoped>
    
</style>