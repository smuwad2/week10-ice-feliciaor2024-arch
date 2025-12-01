<script setup>
import taskTracker from './subcomponents/TaskTracker.vue'
</script>

<script>
    export default {
        data() {
            return {
                desc: '',
                deadline: '',
                taskList: []
            }
        },
        methods: {
            add() {
                this.taskList.push( { 'desc': this.desc, 'deadline': this.deadline } )
                this.desc = ''
                this.deadline = ''
            },
            // TODO: Add a new method, to delete a task completed
            deleteTask(thistask){
                console.log(thistask)
                this.taskList = this.taskList.filter(task => !(task.desc === thistask.desc && task.deadline === thistask.deadline))
            }
            
        },
        components: {
            taskTracker
        }
    }

</script>

<template>
    <div class="mb-3">
        <label for="desc" class="form-label">Task</label>
        <input type="text" class="form-control" id="desc" v-model='desc' placeholder="task">
    </div>
    <div class="mb-3">
        <label for="deadline" class="form-label">Deadline</label>
        <input type="date" class="form-control" id="deadline" v-model='deadline' placeholder="deadline">
    </div>

    <button type="button" @click="add" class="btn btn-primary">Add New Task</button>
    <hr>

    <!-- TODO: Modify following code -->
    <task-tracker v-for="task of taskList" :key = "task.desc" :task = "task" :task.desc="task.desc" :task.deadline="task.deadline" v-on:deleteTask="deleteTask(task)">
    </task-tracker>

</template>

<style scoped>
   
</style>
