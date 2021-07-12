
<!-- [ template ] -->
<template>

    <!-- button: add task -->
    <AddButton />

    <!-- taskboard -->
    <div class="taskboard">
        <h2>Taskboard.</h2>

        <Tasks :tasks="tasks.plans" />
        <Tasks :tasks="tasks.inprogress" />
        <Tasks :tasks="tasks.complete" />
    </div>

</template>


<!-- [ scripts ] -->
<script>
import AddButton from './buttons/AddButton'
import Tasks from './tasks/Tasks'

export default {
    name: 'Taskboard',
    components: {
        AddButton,
        Tasks,
    },
    props: {
        tasks: Object
    }
}
</script>

