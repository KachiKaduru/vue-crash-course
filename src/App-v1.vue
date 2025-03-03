<script>
export default {
  data() {
    return {
      name: "John Doe",
      status: "pending",
      tasks: ["task one", "task two", "task three"],
      link: "https://google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>

<template>
  <div>
    <h1>Vue Jobs</h1>
    <p>{{ name }}</p>
    <p v-if="status === 'active'">Status is active</p>
    <p v-else-if="status === 'pending'">Status is pending</p>
    <p v-else>Status is inactive</p>

    <h3>tasks</h3>
    <ul>
      <li v-for="task in tasks">{{ task }}</li>
    </ul>

    <button @click="toggleStatus">Click to change status</button>
    <br />
    <a :href="link">Go to Google</a>
  </div>
</template>
