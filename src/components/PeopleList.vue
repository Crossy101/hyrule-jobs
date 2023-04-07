<template>
    <div class="container text-center">
        <div class="row row-cols-auto">
            <div v-for="person in randomPeople" :key="person.id.value" class="col">
                <div  class="card" style="width: 18rem;">
                    <img v-bind:src="person.picture.large" class="card-img-top" alt="">
                    <div class="card-body">
                        <h5 class="card-title">{{ person.name.title }} {{ person.name.first }} {{ person.name.last }}</h5>
                        <p>{{ person.dob.age }} Years old</p>
                        <p class="card-text">{{ person.email }}</p>
                        <a href="#" class="btn btn-primary">More Info</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, Prop, PropType } from 'vue'
import RandomPeople, { Person } from '@/types/RandomPeople'

export default defineComponent({
    props: {
        randomPeople: {
            type: Array as PropType<Array<Person>>,
            required: true
        }
    }
})
</script>

<style scoped>
.card {
    margin: 2%;
}
</style>