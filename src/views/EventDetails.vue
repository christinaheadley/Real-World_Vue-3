<template>
  <div v-if="event">
    <!-- v-if added so null isn't returned before api call finishes -->
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script>
import EventService from "../services/EventService.js";
export default {
  props: ["id"],
  data() {
    return {
      event: null,
    };
  },
  created() {
    EventService.getEvent(this.id)
      .then((response) => {
        // console.log("events:", response.data);
        this.event = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>
