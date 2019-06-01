<template>
    <div>
        <b-table :items="people"
                 :fields="fields"
                 striped
                 hover
                 :per-page="perPage"
                 :current-page="currentPage">
            <template slot="deletePerson" slot-scope="row">
                <b-button size="sm" @click="deletePerson(row.item.id, row.index)">
                    Delete
                </b-button>
            </template>
        </b-table>
        <b-pagination
                v-model="currentPage"
                :total-rows="rows"
                :per-page="perPage"
                aria-controls="my-table"
                class="centre"
        ></b-pagination>
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
                'id',
                { firstName    : { sortable: true } },
                { lastName     : { sortable: true } },
                { age          : { sortable: true } },
                { deletePerson : { label: "Delete" } }
            ],
            perPage: 10,
            currentPage: 1,
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
                    this.people.splice(i, 1);
                });
        }
    },
    computed: {
        rows() {
            return this.people.length
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
