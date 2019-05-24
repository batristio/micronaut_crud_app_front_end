<template>
    <div class="hello">
        <div v-for="(person, i) in people" v-bind:key="person">
            <span>First Name: {{ person.firstName }}</span><br/>
            <span>Last Name: {{ person.lastName }}</span><br/>
            <span>Age: {{ person.age }}</span><br/>
            <span>Id: {{ person.id }}</span><br/>
            <button v-on:click="deletePerson(person.id, i)">x</button><br/>
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
        axios
            .get('http://192.168.1.173:8086/person/list/')
            .then(response => {
            this.people = response.data;
        });
    },
    methods: {
        deletePerson(id, i) {
            axios
                .delete('http://192.168.1.173:8086/person/delete/' + id)
                .then(() => {
                    this.people.slice(i, 1);
                });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
