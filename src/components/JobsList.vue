<template>
  <div class="job-list">
    <p>Orded by {{ order }}</p>

    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <img src="../assets/rupee.svg" alt="rupee icon" />
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Molestiae, harum quaerat dolores
          vel amet accusamus necessitatibus maxime at. Minima, architecto. Exercitationem rerum
          voluptatem expedita facilis eligendi totam quaerat. Blanditiis, dignissimos?
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import Job from '../types/Job'
import OrderTerm from '../types/OrderTerm'

const props = defineProps<{
  jobs: Job[]
  order: OrderTerm
}>()

const orderedJobs = computed(() => {
  return [...props.jobs].sort((a: Job, b: Job) => {
    return a[props.order] > b[props.order] ? 1 : -1
  })
})
</script>

<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: rgb(37, 25, 25);
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 30px;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
.list-move {
  transition: all 1s;
}
</style>
