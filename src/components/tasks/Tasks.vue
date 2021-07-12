
<!-- [ template ] -->
<template>
    <!--  -->
    <ul class = 'task-group tasks-plans'>
        <h3 class = 'task-group-title'>{{ title }}</h3>
        <li class = 'task-card' :key="task.id" v-for="task in tasks">
            {{ task.title }}
        </li>
    </ul>
</template>


<!-- [ scripts ] -->
<script>
export default {
    name: 'Tasks',
    components: {
    
    },
    props: {
        title: String,
        tasks: Array,
    }
}
</script>

