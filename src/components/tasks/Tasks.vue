
<!-- [ template ] -->
<template>
    <!-- task group -->
    <ul class = 'task-group tasks-plans'>

        <!-- task group title -->
        <h3 class = 'task-group-title'>{{ title }}</h3>

        <!-- task cards -->
        <li class = 'task-card' :key="task.id" v-for="task in tasks">
            <div class="priority-indicator" :class="task.priority"></div>
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

