<template>
  <div class="app">
    <header>
      <h1 class="title">
        <img :src="require('./assets/Images/heart.svg')" alt="">
        Jobs Finder
      </h1>
      <button @click="handleClick('title')">Order by title</button>
      <button @click="handleClick('salary')">Order by salary</button>
      <button @click="handleClick('location')">Order by location</button>
      <form @submit.prevent>
        <input type="text" v-model="searchWords" placeholder="Search in jobs">
      </form>
    </header>
    <JobsList :jobs="jobs" :order="order" :searchWords="searchWords" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { Job } from "./Helpers/Interfaces";
import { OrderTerm } from "./Helpers/Types";
import JobsList from "./components/JobsList.vue";
export default defineComponent({
  name: "App",
  components: {
    JobsList,
  },
  setup() {
    const jobs = ref<Job[]>([
      {
        title: "Front end developer",
        location: "Egypt",
        salary: 10000,
        id: 1,
      },
      {
        title: "Back-end developer",
        location: "USA",
        salary: 11000,
        id: 2,
      },
      {
        title: "UI/UX designer",
        location: "Saudi Arabia",
        salary: 15000,
        id: 3,
      },
      {
        title: "Cyber security",
        location: "Egypt",
        salary: 20000,
        id: 4,
      },
      {
        title: "Software engineer",
        location: "Palestine",
        salary: 30000,
        id: 5,
      },
      {
        title: "Data analyses",
        location: "Egypt",
        salary: 18000,
        id: 6,
      },
    ]);
    const order = ref<OrderTerm>("title");
    const handleClick = (term: OrderTerm): void => {
      order.value = term;
      return;
    };
    const searchWords = ref<string>("");

    return {
      jobs,
      order,
      searchWords,
      // Methods
      handleClick
    };
  },
});
</script>
<style>
 
</style>