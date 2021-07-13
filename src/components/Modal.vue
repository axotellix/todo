
<!-- [ template ] -->
<template>

    <!-- form: add task -->
    <div class = 'modal' @click='closeModal'>
        <form>
            <!-- heading -->
            <h3 class = 'form-title'>Create new task.</h3>

            <!-- inputs -->
            <label for="description">Description</label>
            <textarea type="text" name = 'description' placeholder = 'Task description ...'></textarea>

            <label for="priority">Priority</label>
            <select name="priority">
                <option value="" selected disabled hidden>Choose priority</option>
                <option value="urgent">Urgent</option>
                <option value="normal">Normal</option>
                <option value="low">Low</option>
            </select>

            <!-- button: create -->
            <Button type='create' />
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
        task: Object
    },
    emits: ['closeModal'],
    methods: {
        closeModal() {
            this.$emit('closeModal'); 
        }
    },
    data() {
        return {
            
        }
    }
}
</script>

