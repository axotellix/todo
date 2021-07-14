
<!-- [ template ] -->
<template>
    <EditModal v-if="show_edit_modal" :task="new_task" @save="save"  @closeModal="closeModal" />
    <Modal v-if="show_modal" :tasks="tasks" @createTask="createTask" @closeModal="closeModal" />
    <Header />
    <Taskboard :tasks="tasks" @setStage="setStage" @openModal="openModal" @editTask="editTask" @deleteTask="deleteTask" />
</template>


<!-- [ scripts ] -->
<script>
import EditModal from './components/EditModal'
import Modal from './components/Modal'
import Header from './components/Header'
import Taskboard from './components/Taskboard'

export default {
    name: 'App',
    components: {
        EditModal,   
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
            this.show_edit_modal = false;
        },
        createTask( new_task ) {
            this.show_modal = false;
            this.tasks.plans.unshift(new_task);
        },
        editTask( id , stage ) {
            // find > task by id & stage
            let get_task = this.tasks[stage].filter(task => task.id == id)[0];

            // get > data
            this.new_task.id = get_task.id;
            this.new_task.description = get_task.description;
            this.new_task.priority = get_task.priority;
            this.new_task.stage = get_task.stage;

            // open > edit Modal
            this.show_edit_modal = true;
        },
        save( edit_task ) {
            // get > Date Object
            let d = new Date();
            function dd( x ) {
                return x < 10 ? ('0' + x) : x;
            }

            // find > task & change > data
            for( let task of this.tasks[edit_task.stage] ) {
                if( task.id == edit_task.id ) {
                    task.id = edit_task.id;
                    task.description = edit_task.description;
                    task.priority = edit_task.priority;
                    task.stage = edit_task.stage;
                    task.date = `${dd(d.getHours())}:${dd(d.getMinutes())}, ${dd(d.getDate())}.${dd(d.getMonth())}.${d.getFullYear()}`;
                }
            } 
            
            // close > edit modal
            this.show_edit_modal = false;
        },
        setStage( id , prev_stage , next_stage ) {
            // remove > task from prev stage
            let prev_task = this.tasks[prev_stage].filter(task => task.id == id)[0];
            this.tasks[prev_stage] = this.tasks[prev_stage].filter(task => task.id != id);

            // add > prev task to next stage
            prev_task.stage = next_stage;
            if( prev_stage != next_stage ) {
                prev_task.id = this.tasks[next_stage + '_id'] + 1;
                this.tasks[next_stage + '_id'] += 1;
            }
            this.tasks[next_stage].push(prev_task);
        },
        deleteTask( id , stage ) {
            this.tasks[stage] = this.tasks[stage].filter(task => task.id != id);
        }
    },
    data() {
        return {
            show_modal: false,
            show_edit_modal: false,
            new_task: {
                id: 1, 
                description: '',
                priority: '',
                stage: 'plans',
                date: '00:00, 01.01.2000'
            },
            tasks: {
                // set > array of tasks
                plans: [],
                inprogress: [],
                complete: [],
                // keep > current task max index [incremented]
                plans_id:       2,
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

