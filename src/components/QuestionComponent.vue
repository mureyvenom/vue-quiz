<script lang="ts">
import Answer from './AnswerComponent.vue';
export default {
  name: 'QuestionComponent',
  components: {
    Answer,
  },
  props: {
    questions: {
      type: Array<{ q: string; answers: Array<{ text: string; is_correct: boolean }> }>,
      required: true,
      default: () => [],
    },
    questionsAnswered: {
      type: Number,
      required: true,
    },
  },
  methods: {
    selectAnswer(is_correct: boolean) {
      this.$emit('question-answered', is_correct);
    },
  },
  emits: ['question-answered'],
};
</script>
<template>
  <div class="relative w-full">
    <div class="h-[50px] mt-2 bg-[#ddd] relative">
      <div
        class="h-full bg-[#ff6372] transition-all duration-300"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="absolute top-[12px] left-0 text-center text-white w-full">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <TransitionGroup name="fade">
      <div
        class="relative w-full"
        v-for="(question, qi) in questions"
        :key="question.q"
        v-show="questionsAnswered === qi"
      >
        <div class="w-full p-5 text-3xl font-bold text-center text-white bg-[#00ca8c] box-border">
          {{ question.q }}
        </div>
        <div class="answers">
          <Answer
            @click="selectAnswer(answer.is_correct)"
            v-for="answer in question.answers"
            :key="answer.text"
            >{{ answer.text }}</Answer
          >
        </div>
      </div>
    </TransitionGroup>
  </div>
</template>

<style scoped></style>
