
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
            <span @click="setPriority($event)" data-priority = 'urgent'>Urgent</span>
            <span @click="setPriority($event)" data-priority = 'normal'>Normal</span>
            <span @click="setPriority($event)" data-priority = 'low'>Low</span>
            
            <span @click="setPriority($event)" data-priority = 'all' class="inactive" v-if="prior_filter">All</span>
        </div></div>

        <!-- task groups -->
        <Tasks 
            @setStage="setStage" 
            @deleteTask="deleteTask" 
            @editTask="editTask" :title="'Planned (' + this.c.plans + ')'"           
            stage="plans"      
            :tasks="tasks.plans" 
            :priorities="priors"     
        />
        <Tasks 
            @setStage="setStage"
            @deleteTask="deleteTask"
            @editTask="editTask" :title="'In-Progress (' + this.c.inprogress + ')'"  
            stage="inprogress"
            :tasks="tasks.inprogress"
            :priorities="priors"   
        />
        <Tasks 
            @setStage="setStage"
            @deleteTask="deleteTask"
            @editTask="editTask" :title="'Complete (' + this.c.complete + ')'" 
            stage="complete"      
            :tasks="tasks.complete"   
            :priorities="priors"  
        />
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
    emits: ['openModal', 'editTask', 'setStage', 'deleteTask'],
    methods: {
        openModal() {
            this.$emit('openModal');
        },
        editTask( id , stage ) {
            this.$emit('editTask', id, stage);
        },
        setStage( id , prev_stage , next_stage ) {
            this.$emit('setStage', id, prev_stage, next_stage);
        },
        deleteTask( id , stage ) {
            this.$emit('deleteTask', id, stage);
        },
        setPriority( e ) {
            // get > priority selected
            let priority = e.target.getAttribute('data-priority');

            if( priority != 'all') {
                // fade > other controls
                e.target.parentNode.querySelectorAll('span').forEach(p => {
                    p.classList.add('inactive');
                });
                e.target.classList.remove('inactive');

                // show > "select all" control
                this.prior_filter = true;

                // set > active priority
                this.priors = [priority];

            } else {
                // hide > "select all" control
                this.prior_filter = false;

                // fade in > all controls
                e.target.parentNode.querySelectorAll('span').forEach(p => {
                    p.classList.remove('inactive');
                });

                // set > active priority
                this.priors = ['urgent', 'normal', 'low'];
            }
        }
    },
    data() {
        return {
            // set > tasks counter
            c: {
                plans:      this.tasks.plans.length,
                inprogress: this.tasks.inprogress.length,
                complete:   this.tasks.complete.length,
            },

            // set > priorities array
            priors: ['urgent', 'normal', 'low'],
            prior_filter: false,
        }
    },
    updated() {
        // set > tasks counter
        this.c.plans = this.tasks.plans.length;
        this.c.inprogress = this.tasks.inprogress.length;
        this.c.complete = this.tasks.complete.length;
    }
}
</script>

