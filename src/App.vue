<template>
 <header><img src="./images/logo.png" class="logo">What's Next?</header>
<div id="container">
    <div id="input-fields">
        <form @submit.prevent="addNewReminder">
            <input type="text" placeholder="Business meeting with bob..." class="reminder-input" v-model="newReminder" name="newTodo">
            <button type="submit" class="btn submit">Submit</button>
        </form>
    </div>
    <h2>Upcoming Reminders</h2>
    <div id="reminder-container">
       <ul class="reminder">
        <li v-for="(reminder, index) in reminders" :key="reminder.id" class="reminder-text">{{reminder.content}} - <button class="btn blue">Edit</button><button class="btn red" @click="removeReminder(index)">Delete</button></li>
       </ul>
    </div>
</div>
    <footer>Created by <a href="#">BeardedWrench</a> - &copy; 2020</footer>
</template>

<script>
import { ref } from 'vue';
export default {
  setup() {
    const newReminder = ref('');
    const reminders = ref([]);
    function addNewReminder() {
      reminders.value.push({
        id: Date.now(),
        done: false,
        content: newReminder.value,
      });
      newReminder.value = '';
    }
    function toggleDone(reminder) {
      reminder.done = !reminder.done;
    }
    function removeReminder(index) {
      reminders.value.splice(index, 1);
    }
    return {
      reminders,
      newReminder,
      addNewReminder,
      toggleDone,
      removeReminder,
    };
  }
}
</script>
