<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <Person/>
  </div>
</template>

<script>
    import Person from './components/Person.vue'
    export default {
        name: 'app',
        components: {
            Person
        }
    }
</script>
