<script setup>
import { ref } from 'vue';

const tasks = ref([{
    name: `Task 1`,
    time: 30
}, {
    name: `Task 2`,
    time: 40
}, {
    name: `Task 3`,
    time: 60
}, {
    name: `Task 4`,
    time: 45
}, {
    name: `Task 5`,
    time: 50
}]);


const editedTask = ref({ name: '', time: 0 });

const selectedTask = ref(null)

const OpenModal = ref(false);

function editTask(index){
    OpenModal.value = true
    selectedTask.value = index
    editedTask.value = {...tasks.value[index]}
    this.tasks.push({name: newTaskName.value, time: newTaskTime.value})
}

function updateTask(){
    OpenModal.value = false
}

</script>
<template>
    <div class="h-100 w-full flex items-center justify-center bg-teal-lightest font-sans mt-20">
        <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
            <div class="mb-4 flex justify-between items-center border-b pb-4">
                <div>
                    <h1 class="text-grey-darkest font-bold">Todo List</h1>
                    <small class="text-gray-600"><span class="font-semibold">N.B: </span>Complete Task in Time</small>
                </div>
            </div>
            <div>
                <div v-for="(task, index) in tasks" :key="index" class="flex mb-4 items-center">
                    <div class="w-full">
                        <p class="w-full text-grey-darkest text-left">{{ task.name }}</p>
                        <small class="block text-gray-700">Complete the Task Within <span class="font-semibold">{{ task.time }}</span> Minute</small>
                    </div>
                    <button @click="editTask(index)" class="flex-no-shrink p-2 ml-2 rounded bg-blue-500 hover:bg-blue-600 text-white hover:text-white">Edit</button>
                </div>
            </div>
        </div>
    </div>
    <transition name="modalTransition">
        <div v-show="OpenModal" class="relative z-10" aria-labelledby="modal-title" role="dialog" aria-modal="true">
            <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>

            <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
                <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
                    <div class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
                        <form @submit.prevent="updateTask(index)">
                            <div class="bg-white px-4 pb-4 pt-5 sm:p-6 sm:pb-4">
                                <div class="sm:flex sm:items-start">
                                    <div class="mt-3 text-center sm:text-left">
                                        <h3 class="text-base font-semibold leading-6 text-gray-900" id="modal-title">Edit Task</h3>
                                    </div>
                                </div>
                                <div class="mt-2">
                                    <label for="taskName" class="block text-sm font-medium leading-6 text-gray-900">Task Name</label>
                                    <div class="relative mt-2 rounded-md shadow-sm">
                                        <input v-model="editedTask.name" type="text" name="taskName" id="taskName" class="block w-full rounded-md border-0 py-1.5 pl-3 pr-20 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:outline-none sm:text-sm sm:leading-6" placeholder="Ex: Create a Todo List">
                                    </div>
                                </div>
                                <div class="mt-2">
                                    <label for="time" class="block text-sm font-medium leading-6 text-gray-900">Time (in Minutes)</label>
                                    <div class="relative mt-2 rounded-md shadow-sm">
                                        <input v-model="editedTask.time" type="number" name="time" id="time" class="block w-full rounded-md border-0 py-1.5 px-3 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:outline-none sm:text-sm sm:leading-6" placeholder="Ex: 30 Minutes">
                                    </div>
                                </div>
                            </div>
                            <div class="bg-gray-50 px-4 py-3 sm:flex sm:flex-row-reverse sm:px-6">
                                <button @click="toggleModal" type="submit" class="inline-flex w-full justify-center rounded-md bg-green-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-green-500 sm:ml-3 sm:w-auto">Update Task</button>
                                <button @click="toggleModal" type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:mt-0 sm:w-auto">Cancel</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>