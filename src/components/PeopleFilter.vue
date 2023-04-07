<template>
    <div class="container text-center">
        <div class="row row-cols-2">
            <div class="col-2">
                <input v-model="filter.nameSearch" @keyup="OnPeopleSearch" type="text" class="form-control" placeholder="Search" aria-label="Search" aria-describedby="basic-addon1">
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue'
import $ from 'jquery';
import PeopleListFilter from '@/types/PeopleListFilter';

export default defineComponent({

    setup() {
        const state = reactive({
            filter: {} as PeopleListFilter
        });

        return {...toRefs(state)};
    },
    props: {
        RandomPeopleFilterUpdate: {
            type: Function,
            required: true
        }
    },
    methods: {
        OnPeopleSearch() {
            this.RandomPeopleFilterUpdate(this.filter);
        }
    }
})
</script>

<style scoped>

</style>