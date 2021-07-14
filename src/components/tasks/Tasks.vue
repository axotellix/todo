
<!-- [ template ] -->
<template>
    <!-- task group -->
    <ul 
        class = 'task-group tasks-plans' 
        @drop="onDrop($event, tasks[0])"
        @dragover.prevent
    >

        <!-- task group title -->
        <h3 class = 'task-group-title'>{{ title }}</h3>

        <!-- task cards -->
        <li class = 'task-card' 
            :data-id="task.id" 
            :key="task.id" 
            v-for="task in tasks"
            draggable='true'
            @dragstart="startDrag($event, task)"
        >
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
                    <svg @click="prevStage($event)" :active="task.stage!='plans'" class="ico arrow-left">
                        <use xlink:href="/img/sprites.svg#ico-arrow"></use>
                    </svg>
                    <!-- control: edit -->
                    <svg @click="editTask($event)" class="ico edit">
                        <use xlink:href="/img/sprites.svg#ico-edit"></use>
                    </svg>
                    <!-- control: move right -->
                    <svg @click="nextStage($event)" v-if="task.stage!='complete'" :active="task.stage!='complete'" class="ico arrow-right">
                        <use xlink:href="/img/sprites.svg#ico-arrow"></use>
                    </svg>
                    <!-- control: move right -->
                    <svg @click="deleteTask($event)" v-if="task.stage=='complete'" active="true" class="ico cross">
                        <use xlink:href="/img/sprites.svg#ico-cross"></use>
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
    emits: ['editTask', 'prevStage', 'nextStage', 'deleteTask'],
    methods: {
        editTask( e ) {                     
            // get > task id & stage
            let node = e.target.parentNode.parentNode.parentNode;   //FIX: get the correct parent node
            let id = node.getAttribute('data-id');
            let stage = this.tasks[0].stage;

            // emit > edit task method
            this.$emit('editTask', id, stage);
        },
        prevStage( e ) {
            // get > task id & stage
            let node = e.target.parentNode.parentNode.parentNode;   //FIX: get the correct parent node
            let id = node.getAttribute('data-id');
            let prev_stage = this.tasks[0].stage;
            let next_stage = prev_stage;


            if( prev_stage == 'inprogress' ) next_stage = 'plans';
            if( prev_stage == 'complete' ) next_stage = 'inprogress';

             // emit > edit task method
            this.$emit('setStage', id, prev_stage, next_stage);
        },
        nextStage( e ) {
            // get > task id & stage
            let node = e.target.parentNode.parentNode.parentNode;   //FIX: get the correct parent node
            let id = node.getAttribute('data-id');
            let prev_stage = this.tasks[0].stage;
            let next_stage = prev_stage;

            if( prev_stage == 'plans' ) next_stage = 'inprogress';
            if( prev_stage == 'inprogress' ) next_stage = 'complete';

             // emit > edit task method
            this.$emit('setStage', id, prev_stage, next_stage);
        },
        deleteTask( e ) {
            // get > task id & stage
            let node = e.target.parentNode.parentNode.parentNode;   //FIX: get the correct parent node
            let id = node.getAttribute('data-id');
            let stage = this.tasks[0].stage;

             // emit > edit task method
            this.$emit('deleteTask', id, stage);
        },
    },
    setup(props, { emit }) {
        const startDrag = ( e , item ) => {
            e.dataTransfer.dropEffect = 'move';
            e.dataTransfer.effectAllowed = 'move';
            e.dataTransfer.setData('id', item.id.toString());
            e.dataTransfer.setData('prev_stage', item.stage.toString());
        }

        const onDrop = ( e , item ) => {
            let id = e.dataTransfer.getData('id');
            let prev_stage = e.dataTransfer.getData('prev_stage');
            let next_stage = item.stage;

             // emit > edit task method
            emit('setStage', id, prev_stage, next_stage);
        }

        return {
            startDrag,
            onDrop,
        }
    }
}
</script>

