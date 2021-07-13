
<!-- [ template ] -->
<template>

    <!-- button: add task -->
    <Button type="add" @click="openModal" />

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
        <Tasks @editTask="editTask" :title="'Planned (' + this.c.plans + ')'"           :tasks="tasks.plans"      />
        <Tasks @editTask="editTask" :title="'In-Progress (' + this.c.inprogress + ')'"  :tasks="tasks.inprogress" />
        <Tasks @editTask="editTask" :title="'Complete (' + this.c.complete + ')'"       :tasks="tasks.complete"   />
    </div>

</template>


<!-- [ scripts ] -->
<script>
import Button from './buttons/Button'
import Tasks from './tasks/Tasks'

export default {
    name: 'Taskboard',
    components: {
        Button,
        Tasks,
    },
    props: {
        tasks: Object
    },
    emits: ['openModal', 'editTask'],
    methods: {
        openModal() {
            this.$emit('openModal');
        },
        editTask( id , stage ) {
            this.$emit('editTask', id, stage);
        }
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

