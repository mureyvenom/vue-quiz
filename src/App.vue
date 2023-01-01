<script lang="ts">
import Question from './components/QuestionComponent.vue';
import Result from './components/ResultComponent.vue';
export default {
  name: 'App',
  components: {
    Question,
    Result,
  },
  data() {
    return {
      questions: [
        {
          q: 'What is 2 + 2?',
          answers: [
            {
              text: '4',
              is_correct: true,
            },
            {
              text: '3',
              is_correct: false,
            },
            {
              text: 'Fish',
              is_correct: false,
            },
            {
              text: '5',
              is_correct: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: '5',
              is_correct: false,
            },
            {
              text: '7',
              is_correct: false,
            },
            {
              text: '6',
              is_correct: true,
            },
            {
              text: '12',
              is_correct: false,
            },
          ],
        },
        {
          q: 'Find the missing letter: C_ke',
          answers: [
            {
              text: 'e',
              is_correct: false,
            },
            {
              text: 'a',
              is_correct: true,
            },
            {
              text: 'i',
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: 'Try again!',
          desc: 'Do a little more studying and you may succeed!',
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: 'Studying has definitely paid off for you!',
        },
      ],
      questionsAnswered: 0,
      totalCorrect: 0,
    };
  },
  methods: {
    questionAnswered(is_correct: boolean) {
      if (is_correct) {
        this.totalCorrect++;
      }
      this.questionsAnswered++;
    },
    resetQuiz() {
      this.totalCorrect = 0;
      this.questionsAnswered = 0;
    },
  },
};
</script>

<template>
  <div class="mx-auto my-0 max-w-[600px] w-full box-border relative">
    <Transition name="fade" mode="out-in">
      <Question
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <Result :results="results" :totalCorrect="totalCorrect" v-else />
    </Transition>
    <button
      @click.prevent="resetQuiz"
      type="button"
      class="bg-[#ff6372] border-0 text-xl text-white py-2 px-6 my-2 mx-auto"
    >
      Reset
    </button>
  </div>
</template>
