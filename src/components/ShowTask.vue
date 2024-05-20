<template>     
    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
        <Trash v-if="isChecked && tasks.length > 0" @click="emitFunction"/>
        <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400 mt-4">
            <thead class="text-xs text-gray-700 uppercase  dark:bg-gray-700 dark:text-gray-400">
                <tr>
                    <th scope="col" class="p-4">
                        <div class="flex items-center">
                            <input v-model="isChecked" @change="handleIschecked" :disabled="tasks.length == 0" id="checkbox-all-search" type="checkbox" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                            <label for="checkbox-all-search" class="sr-only">checkbox</label>
                        </div>
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Tasks
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Actions
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Status
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="taskObject in tasks" :key="taskObject.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                    <td class="w-4 p-4">
                        <div class="flex items-center">
                            <input id="checkbox-table-search-1" type="checkbox" class="inputChecked w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                            <label for="checkbox-table-search-1" class="sr-only">checkbox</label>
                        </div>
                    </td>
                    <th   scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        {{ taskObject.task }}
                    </th>
                    <td class="px-6 py-4 flex gap-8">
                        <Check v-if="!taskObject.completed" @click="handleClick(taskObject)"/>
                        <Trash @click="$emit('deleteTask', taskObject.id)" />
                    </td>
                    <td class="px-6 py-4 ">
                        <span v-if="taskObject.completed" class="flex items-center gap-2">Completed <Check /></span>
                        <span v-else class="flex items-center gap-2">No completed <Cross /></span>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { ref } from "vue";
import Check from "./icons/Check.vue";
import Cross from "./icons/Cross.vue";
import Trash from './icons/Trash.vue';

const props = defineProps(['tasks'])
let isChecked = ref(false)
const emit = defineEmits(['deleteAllTasks'])

const handleClick = (taskObject) => {
    taskObject.completed = true
}
const handleIschecked = () => {
    const inputsCheckbox = document.querySelectorAll('.inputChecked')
    
    inputsCheckbox.forEach(input => {
        input.checked = isChecked.value
    })
}
const emitFunction = () => {
    emit('deleteAllTasks')
    isChecked.value = false
}
</script>

<style scoped>

</style>