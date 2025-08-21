<script setup lang="ts">
import { ref } from "vue";
import axios from "axios";

const question_text = ref<string>('');
const answer_text = ref<string>('');

async function save() {
  if (question_text.value.trim() === '' || answer_text.value.trim() === '') {
    alert('Bitte fülle beide Felder aus.');
    return;
  }

  try {
    const response = await axios.post('http://127.0.0.1:5000/simple_question', {
      question: question_text.value,
      answer: answer_text.value
    });
    console.log('Erfolg:', response.data);
    question_text.value = '';
    answer_text.value = '';
  } catch (error) {
    console.error('Fehler:', error);
    alert('Fehler beim Speichern. Siehe Konsole für Details.');
  }
}
</script>

<template>
  <input type="text" v-model="question_text" placeholder="Frage" />
  <input v-model="answer_text" placeholder="Antwort" />
  <button @click="save">Speichern</button>
</template>

<style scoped></style>
