<template>
    <PeopleFilter :RandomPeopleFilterUpdate="RandomPeopleFilterUpdate" />
    <PeopleList :randomPeople="allPeople"  />
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue'
import PeopleFilter from './PeopleFilter.vue';
import PeopleList from './PeopleList.vue';
import PeopleListFilter from '@/types/PeopleListFilter';
import RandomPeople, { Person } from '@/types/RandomPeople';
import $ from 'jquery';


export default defineComponent({
    setup() {
        const state = reactive({
            allData: {} as RandomPeople,
            allPeople: {} as Array<Person>
        });

        return { ...toRefs(state) };      
    },
    mounted() {
        this.GetRandomPeopleData();
    },  
    components: {
        PeopleFilter,
        PeopleList
    },
    methods: {
        GetRandomPeopleData(amountOfPeople = 20) {
            fetch(`https://randomuser.me/api?results=${amountOfPeople}`)
                .then(response => response.json())
                .then(data => (this.allData = data))
                .then(() => (
                    this.allPeople = $.extend(true, [], this.allData.results)
                ))
        },
        RandomPeopleFilterUpdate(filter: PeopleListFilter)
        {
            this.allPeople = $.extend(true, [], this.allData.results);

            if(filter.nameSearch)
            {
                this.allPeople = this.allPeople.filter(currentPerson => 
                    (currentPerson.name.title + " " + currentPerson.name.first + " " + currentPerson.name.last).includes(filter.nameSearch)
                );
            }
        }
    }

})
</script>

<style lang="less" scoped>

</style>
