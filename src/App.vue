
<!-- [ template ] -->
<template>
    <Modal v-if="this.show_modal" @closeModal="closeModal" />
    <Header />
    <Taskboard :tasks="tasks" @openModal="openModal" />
</template>


<!-- [ scripts ] -->
<script>
import Modal from './components/Modal'
import Header from './components/Header'
import Taskboard from './components/Taskboard'

export default {
    name: 'App',
    components: {
        Modal,   
        Header,   
        Taskboard,   
    },
    methods: {
        openModal() {
            this.show_modal = true;
        },
        closeModal() {
            this.show_modal = false;
        },
    },
    data() {
        return {
            show_modal: false,
            tasks: {
                plans: [],
                inprogress: [],
                complete: [],
            },
            priorities: {
                urgent: 'urgent',
                normal: 'normal',
                low:    'low',
            }
        }
    },
    created() {
        // fill > planned tasks
        this.tasks.plans = [
            {
                id: 1, 
                title: 'plan_1', 
                description: 'Lorem ipsum dolor site amet consectetur adipisci elit.',
                priority: this?.priorities?.urgent ?? 'no-prior',
                stage: 'plans'
            },
            {
                id: 2, 
                title: 'plan_2', 
                description: 'description',
                priority: this?.priorities?.normal ?? 'no-prior',
                stage: 'plans'
            },
            {
                id: 3, 
                title: 'plan_3', 
                description: 'description',
                priority: this?.priorities?.low ?? 'no-prior',
                stage: 'plans'
            },
        ];

        // fill > in-progress tasks
        this.tasks.inprogress = [
            {id: 1, title: 'inprogress_1', description: 'description'},
            {id: 2, title: 'inprogress_2', description: 'description'},
        ];

        // fill > complete tasks
        this.tasks.complete = [
            {id: 1, title: 'complete_1', description: 'description', stage: 'complete'},
            {id: 2, title: 'complete_2', description: 'description'},
        ];
    }
}
</script>

