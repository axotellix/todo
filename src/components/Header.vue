
<!-- [ template ] -->
<template>
    <header class = 'header'>
        <!-- [ logo ] -->
        <span class="logo">TD.</span>

        <!-- [ project name ] -->
        <h1>ToDo</h1>

        <!-- [ dark / light theme switcher ] -->
        <div class="theme-controller">
            <a @click="setTheme('night')" class = 'night active'>night</a> 
            <span>/</span>
            <a @click="setTheme('light')" class='light'>light</a>
        </div>
    </header>
</template>


<!-- [ scripts ] -->
<script>
export default {
    name: 'Header',
    components: {
    
    },
    methods: {
        setTheme( theme ) {
            if( theme === 'night' ) {
                document.querySelector('.light').classList.remove('active');
                document.querySelector('.night').classList.add('active');
                document.body.classList.remove('light');
                document.body.classList.add('night');
            }
            if( theme === 'light' ) {
                document.querySelector('.night').classList.remove('active');
                document.querySelector('.light').classList.add('active');
                document.body.classList.remove('night');
                document.body.classList.add('light');
            }
        }
    }
}
</script>

