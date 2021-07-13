
<!-- [ template ] -->
<template>

    <!-- form: edit task -->
    <div class = 'modal' @click.self='closeModal'>
        <form>
            <!-- heading -->
            <h3 class = 'form-title'>Edit task.</h3>

            <!-- inputs -->
            <label for="description">Description</label>
            <textarea v-model="edit_task.description" type="text" name = 'description' placeholder = 'Task description ...'></textarea>

            <label for="priority">Priority</label>
            <select v-model="edit_task.priority" name="priority">
                <option value="" selected disabled hidden>Choose priority</option>
                <option value="urgent">Urgent</option>
                <option value="normal">Normal</option>
                <option value="low">Low</option>
            </select>

            <!-- button: create -->
            <Button type='edit' @click="save( this.edit_task )" />
        </form>
    </div>

</template>


<!-- [ scripts ] -->
<script>
import Button from './buttons/Button'

export default {
    name: 'EditModal',
    components: {
        Button
    },
    props: {
        task: Object
    },
    emits: ['closeModal', 'save'],
    methods: {
        closeModal() {
            this.$emit('closeModal'); 
        },
        save( task ) {
            this.$emit('save', task);
        }
    },
    data() {
        return {
            edit_task: {
                id: 1, 
                description: '',
                priority: '',
                stage: 'plans',
                date: '00:00, 01.01.2000'
            }
        }
    },
    created() {
        this.edit_task.id = this.task.id;
        this.edit_task.description = this.task.description;
        this.edit_task.priority = this.task.priority;
        this.edit_task.stage = this.task.stage;
    }
}
</script>

