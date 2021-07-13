
<!-- [ template ] -->
<template>
    <!-- task group -->
    <ul class = 'task-group tasks-plans'>

        <!-- task group title -->
        <h3 class = 'task-group-title'>{{ title }}</h3>

        <!-- task cards -->
        <li class = 'task-card' :data-id="task.id" :key="task.id" v-for="task in tasks">
            <!-- priority indicator -->
            <div class="priority-indicator" :class="task.priority"></div>

            <!-- task title -->
            <h4 class = 'task-title'>
                <span>Task:</span> #{{ task.id }}
            </h4>
            
            <!-- task description -->
            <p class = 'task-description'>
                {{ task.description }}
            </p>

            <div class="task-footer">
                <!-- creation date -->
                <span class = 'task-date'>
                    {{ task.date ?? '00:00, 01.01.2000' }}
                </span>
                <!-- task controls -->
                <div class="task-controls">
                    <!-- control: move left -->
                    <svg :active="task.stage!='plans'" class="ico arrow-left">
                        <use xlink:href="/img/sprites.svg#ico-arrow"></use>
                    </svg>
                    <!-- control: edit -->
                    <svg @click="editTask($event)" class="ico edit">
                        <use xlink:href="/img/sprites.svg#ico-edit"></use>
                    </svg>
                    <!-- control: move right -->
                    <svg :active="task.stage!='complete'" class="ico arrow-right">
                        <use xlink:href="/img/sprites.svg#ico-arrow"></use>
                    </svg>
                </div>
            </div>
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
    },
    emits: ['editTask'],
    methods: {
        editTask( e ) {                     
            // get > task id & stage
            let node = e.target.parentNode.parentNode.parentNode;   //FIX: get the correct parent node
            let id = node.getAttribute('data-id');
            let stage = this.tasks[0].stage;

            // emit > edit task method
            this.$emit('editTask', id, stage);
        }
    }
}
</script>

