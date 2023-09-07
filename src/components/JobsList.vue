<template>
  <div class="job-list">
    Ordered By: <strong>{{ order }}</strong>
    <TransitionGroup name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>
          {{ job.title }}
          in
          {{ job.location }}
        </h2>
        <div>
          <div class="salary">
            <img :src="require('../assets/Images/rupee.svg')" alt="" />
            <p>{{ job.salary }} EGP</p>
          </div>
          <div class="description">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Assumenda
            quas architecto earum illo sapiente aperiam cupiditate reprehenderit
            quia. Dolores neque officiis animi deleniti. Provident, facilis
            velit quas dolores doloribus beatae ducimus consequuntur dicta earum
            possimus dolorem. Accusantium, ea perferendis neque quidem quo
            cupiditate perspiciatis quos commodi minima illo a numquam?
          </div>
        </div>
      </li>
    </TransitionGroup>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import { Job } from "../Helpers/Interfaces";
import { OrderTerm } from "../Helpers/Types";

export default defineComponent({
  name: "JobsList",
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
    searchWords:{
      required: true,
      type: String,
    }
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].filter(el => el.title.toLocaleLowerCase().includes(props.searchWords.toLocaleLowerCase())).sort((a: Job, b: Job): number => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });

    return {
      orderedJobs,
    };
  },
  //   setup(props) {},
});
</script>

<style scoped>
.list-move {
  transition: all 0.5s;
}
</style>
