<script setup>
import { onMounted, ref, watch, computed, onUpdated } from "vue";
import HappyWeekend from "./HappyWeekend.vue";

const question = ref("");
const answer = ref("Ask your question. 🧐");
const title = ref("I have feeling this going to be...");
const image = ref("");


// ignore this line
// const props = defineProps({
//   name: String
// })

// methods
const getQuestion = async () => {
  try {
    const res = await fetch("https://yesno.wtf/api");
    return await res.json();
  } catch (error) {
    return "Error! Could not reach the API. " + error;
  }
};

// lifecycle hooks
onMounted(() => {
  var feeling = "";
  setTimeout(async () => {
    feeling = await getQuestion();
    switch (feeling.answer) {
      case "yes":
        title.value = "I got a feeling that tonight's gonna be a good night 🎉";
        break;
      case "no":
        title.value = "I got a bad bad feeling about this 🤢";
        break;
      default:
        title.value = "You are a robot 🤖";
        break;
    }
  }, 1000);
});

onUpdated(() => {
  console.log('There is change somewhere...')
})

// computed
const answerHelper = computed(() => {
  var helper = "";
  switch (answer.value) {
    case "yes":
      helper = "🎉";
      break;
    case "no":
      helper = "❌";
      break;
    default:
      helper = "";
      break;
  }
  return helper;
});

// watch works directly on a ref
watch(question, (newQuestion) => {
  if (newQuestion.indexOf("?") > -1) {
    answer.value = "Thinking...";
    setTimeout(async () => {
      var res = await getQuestion();
      answer.value = res.answer;
      image.value = res.image;
    }, 1000);
  } else if (newQuestion.length > 0) {
    answer.value = "Questions usually contain a ❓ mark. 🙄";
    image.value = "";
  } else {
    answer.value = "Ask your question. 🧐";
    image.value = "";
  }
});

</script>

<template>
  <div class="question">
    <h2>{{ title }}</h2>
    <img v-if="image.length > 0" :src="image" alt="image" />
    <p>
      Ask a yes/no question:
      <input v-model="question" />
    </p>
    <p>{{ answer }} {{ answerHelper }}</p>
    <HappyWeekend />
  </div>
</template>

<style>

.question {
  border-top: 1px solid #cacaca;
  padding-top: 30px;
}

img {
  animation: fade-in;
  animation-duration: 500ms;
  animation-delay: 100ms;
}

@keyframes fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>