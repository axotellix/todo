
<!-- [ template ] -->
<template>

    <!-- form: add task -->
    <div class = 'modal' @click.self='closeModal'>
        <form>
            <!-- heading -->
            <h3 class = 'form-title'>Create new task.</h3>

            <!-- inputs -->
            <label for="description">Description</label>
            <textarea v-model="new_task.description" type="text" name = 'description' placeholder = 'Task description ...'></textarea>

            <label for="priority">Priority</label>
            <select v-model="new_task.priority" name="priority">
                <option value="" selected disabled hidden>Choose priority</option>
                <option value="urgent">Urgent</option>
                <option value="normal">Normal</option>
                <option value="low">Low</option>
            </select>

            <!-- button: create -->
            <Button type='create' @click="createTask( this.new_task )" />
        </form>
    </div>

</template>


<!-- [ scripts ] -->
<script>
import Button from './buttons/Button'

export default {
    name: 'Modal',
    components: {
        Button
    },
    props: {
        tasks: Object
    },
    emits: ['closeModal'],
    methods: {
        closeModal() {
            this.$emit('closeModal'); 
        },
        createTask( task ) {
            this.$emit('createTask', task);
        }
    },
    data() {
        return {
            new_task: {
                id: 1, 
                description: '',
                priority: '',
                stage: 'plans',
                date: '00:00, 01.01.2000'
            }
        }
    },
    created() {
        let d = new Date();
        function dd( x ) {
            return x < 10 ? ('0' + x) : x;
        } 

        this.new_task.id = this.tasks.plans_id + 1;
        this.new_task.date = `${dd(d.getHours())}:${dd(d.getMinutes())}, ${dd(d.getDate())}.${dd(d.getMonth())}.${d.getFullYear()}`;
    }
}
</script>

