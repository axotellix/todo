
<!-- [ template ] -->
<template>
    <Modal v-if="this.show_modal" :tasks="tasks" @createTask="createTask" @closeModal="closeModal" />
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
        createTask( new_task ) {
            this.show_modal = false;
            this.tasks.plans.unshift(new_task);
        }
    },
    data() {
        return {
            show_modal: false,
            tasks: {
                // set > array of tasks
                plans: [],
                inprogress: [],
                complete: [],
                // keep > current task max index [incremented]
                plan_id:        2,
                inprogress_id:  1,
                complete_id:    1,
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
                id: 2, 
                description: 'Lorem ipsum dolor site amet consectetur adipisci elit.',
                priority: this?.priorities?.urgent ?? 'no-prior',
                date: '00:00, 01.01.2000',
                stage: 'plans',
            },
            {
                id: 1, 
                description: 'Lorem ipsum dolor site amet consectetur adipisci elit.',
                priority: this?.priorities?.normal ?? 'no-prior',
                date: '00:00, 01.01.2000',
                stage: 'plans'
            },
        ];

        // fill > in-progress tasks
        this.tasks.inprogress = [
            {
                id: 1, 
                description: 'Lorem ipsum dolor site amet consectetur adipisci elit.',
                priority: this?.priorities?.low ?? 'no-prior',
                date: '00:00, 01.01.2000',
                stage: 'inprogress',
            },
        ];

        // fill > complete tasks
        this.tasks.complete = [
             {
                id: 1, 
                description: 'Lorem ipsum dolor site amet consectetur adipisci elit.',
                priority: this?.priorities?.low ?? 'no-prior',
                date: '00:00, 01.01.2000',
                stage: 'complete',
            },
        ];
    }
}
</script>

