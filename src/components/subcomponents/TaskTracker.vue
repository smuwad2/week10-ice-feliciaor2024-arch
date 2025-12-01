<script>
    // TODO: Complete the code
    export default { 
        emit: ['deleteTask'],
        props: ['task']
        // Hint: insert properties task (Object) and idx (Number)
    }
</script>

<template>
    <!-- TODO: add your template code here --> 
     <div class = "card" style = "width:14rem;height:20rem;display:inline-block;vertical-align: top;">
        <div class = "card-body">
            <h5 class = "card-title">Deadline: {{ task.deadline }}</h5>
            <hr></hr>
            <p class = "card-text">{{ task.desc }}</p>
            <button class ="btn btn-primary" @click="$emit('deleteTask')">Done</button>
        </div>
     </div>
   
</template>


