
<!-- [ template ] -->
<template>

    <!-- button: add task -->
    <AddButton />

    <!-- taskboard -->
    <div class="taskboard">
        <!-- taskboard heading -->
        <h2>Taskboard.</h2>

        <!-- priorities guide-->
        <div class="prior-guide"><div>
            <span data-priority = 'urgent'>Urgent</span>
            <span data-priority = 'normal'>Normal</span>
            <span data-priority = 'low'>Low</span>
        </div></div>

        <!-- task groups -->
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

