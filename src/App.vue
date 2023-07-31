<template>
  <h1>CRUD</h1>
  <form @submit.prevent="addNewTopic">
    <label>New Topic</label>
    <input v-model="newTopic" name="newTopic">
    <button>Add New Topic</button>
  </form>
  <button @click="removeAlltopics">Remove All</button>
 
  <ul>
    <li v-for="(topic, index) in topics" :key="topic.id" class="topic">
      <h3 :class="{ done: topic.done }" @click="toggleDone(topic)">{{topic.content}}</h3>
      <button @click="removetopic(index)">Remove Topic</button>
    </li>


  </ul>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTopic = ref('');
    const topics = ref([]);

    function addNewTopic() {
      topics.value.push({
        id: Date.now(),
        done: false,
        content: newTopic.value,
      });
      newTopic.value = '';
    }

    function toggleDone(topic) {
      topic.done = !topic.done;
    }

    function removetopic(index) {
      topics.value.splice(index, 1);
    }

    function removeAlltopics() {
      topics.value = [];
    }


    return {
      topics,
      newTopic,
      addNewTopic,
      toggleDone,
      removetopic,
      removeAlltopics,
    };
  }
}
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
h1{
  text-align: center;
}
input, textarea, button, p, div, section, article, select {
  display: 'block';
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}

.topic {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
ul{
  list-style: none;
}
</style>