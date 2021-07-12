
<!-- [ template ] -->
<template>

    <!-- button: add task -->
    <AddButton />

    <!-- taskboard -->
    <div class="taskboard">
        <h2>Taskboard.</h2>

        <Tasks :title="'Planned (' + this.c.plans + ')'"           :tasks="tasks.plans"      />
        <Tasks :title="'In-Progress (' + this.c.inprogress + ')'"  :tasks="tasks.inprogress" />
        <Tasks :title="'Complete (' + this.c.complete + ')'"       :tasks="tasks.complete"   />
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
    },
    data() {
        return {
            // set > tasks counter
            c: {
                plans:      this.tasks.plans.length,
                inprogress: this.tasks.inprogress.length,
                complete:   this.tasks.complete.length,
            }
        }
    }
}
</script>

