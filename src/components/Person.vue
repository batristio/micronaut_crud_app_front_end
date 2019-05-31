<template>
    <div>
        <b-table :items="people" :fields="fields" striped hover>
            <template slot="deletePerson" slot-scope="row">
                <b-button size="sm" @click="deletePerson(row.id, data.index)">
                    Delete {{ row.value }}
                </b-button>
            </template>
        </b-table>
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
