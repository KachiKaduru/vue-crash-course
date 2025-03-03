<script setup>
import { onMounted, ref } from "vue";

const name = ref("John Doe");
const status = ref("pending");
const tasks = ref(["task one", "task two", "task three"]);
const newTask = ref("");
// const link = ref("https://google.com");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async function () {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await res.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("Error fetching data");
  }
});
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
      <li v-for="task in tasks">
        <span>
          {{ task }}
        </span>
        <span @click="deleteTask">&marker;</span>
      </li>
    </ul>

    <button @click="toggleStatus">Click to change status</button>
    <br />
    <!-- <a :href="link">Go to Google</a> -->

    <form @submit.prevent="addTask">
      <label for="newTask">Add task</label>
      <input type="text" name="newTask" id="newTask" v-model="newTask" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>
