
<!-- [ template ] -->
<template>
   <a class = 'button'>{{ this.types[type] }}</a>
</template>


<!-- [ scripts ] -->
<script>
export default {
    name: 'Button',
    components: {
    
    },
    props: {
        type: String,
    },
    data() {
        return {
            // set > button types (and inner text)
            types: {
                'add': '+ create task',
                'create': 'create',
                'edit': 'save',
            }
        }
    }
}
</script>

