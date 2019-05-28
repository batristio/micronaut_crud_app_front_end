<template>
    <div class="hello">
        <!--<div v-for="(person, i) in people" v-bind:key="i">
            <span>First Name: {{ person.firstName }}</span><br/>
            <span>Last Name: {{ person.lastName }}</span><br/>
            <span>Age: {{ person.age }}</span><br/>
            <span>Id: {{ person.id }}</span><br/>
            <button v-on:click="deletePerson(person.id, i)">x</button><br/>
        </div>-->
        <div>
            <b-table striped hover :items="people" :fields="fields">
                <template slot="show_details">
                    <b-button size="sm" @click="deletePerson(row.id, data.index)" class="mr-2">
                        x
                    </b-button>
                </template>
            </b-table>
        </div>
    </div>
</template>

<script>

import axios from 'axios'

export default {

    name: 'Person',
    data() {
        return {
            people : [],
            fields : [
                { firstName    : { sortable: true } },
                { lastName     : { sortable: true } },
                { age          : { sortable: true } },
                { deletePerson : { label: "Delete" } }
            ],
        };
    },
    created: function () {
        axios
            .get('http://localhost:8086/person/list')
            .then(response => {
            this.people = response.data;
        });
    },
    methods: {
        deletePerson(id, i) {
            axios
                .delete('http://localhost:8086/person/delete/' + id)
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
