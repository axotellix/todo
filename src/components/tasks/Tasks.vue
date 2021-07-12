
<!-- [ template ] -->
<template>
    <ul class = 'task-card tasks-plans'>
        {{ title }}
        <li class = 'task-item' :key="task.id" v-for="task in tasks">
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

