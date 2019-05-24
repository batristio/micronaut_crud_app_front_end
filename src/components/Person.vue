<template>
    <div class="hello">
        <div>
            <ul v-for="person in people" v-bind:key="person">
                <li>First Name: {{ person.firstName }}</li>
                <li>Last Name: {{ person.lastName }}</li>
                <li>Age: {{ person.age }}</li>
                <li>Id: {{ person.id }}</li>
            </ul>
        </div>
    </div>
</template>

<script>

import axios from 'axios'

export default {

    name: 'Person',
    data() {
        return {
            people:[]
        };
    },
    created: function () {
        axios.get('http://192.168.1.173:8086/person/list/')
            .then(response => {
            this.people = response.data;
        });
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
