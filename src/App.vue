
<!-- [ template ] -->
<template>
    <Header />
    <Taskboard :tasks="tasks" />
</template>


<!-- [ scripts ] -->
<script>
import Header from './components/Header'
import Taskboard from './components/Taskboard'

export default {
    name: 'App',
    components: {
        Header,   
        Taskboard,   
    },
    data() {
        return {
            tasks: {
                plans: [],
                inprogress: [],
                complete: [],
            }
        }
    },
    created() {
        // fill > planned tasks
        this.tasks.plans = [
            {id: 1, title: 'plan_1', description: 'description'},
            {id: 2, title: 'plan_2', description: 'description'},
        ];

        // fill > in-progress tasks
        this.tasks.inprogress = [
            {id: 1, title: 'inprogress_1', description: 'description'},
            {id: 2, title: 'inprogress_2', description: 'description'},
        ];

        // fill > complete tasks
        this.tasks.complete = [
            {id: 1, title: 'complete_1', description: 'description'},
            {id: 2, title: 'complete_2', description: 'description'},
        ];
    }
}
</script>

