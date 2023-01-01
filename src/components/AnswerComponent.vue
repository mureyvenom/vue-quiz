<script lang="ts">
export default {
  name: 'AnswerComponent',
  methods: {
    clicked() {
      this.$emit('click');
    },
  },
  emits: ['click'],
};
</script>
<template>
  <div class="answer" @click.prevent="clicked"><slot /></div>
</template>

<style scoped>
.answer {
  border: 1px solid #8e959f;
  padding: 20px;
  font-size: 18px;
  width: 100%;
  background-color: #fff;
  transition: 0.2s linear all;
}
.answer span {
  display: inline-block;
  margin-left: 5px;
  font-size: 0.75em;
  font-style: italic;
}
.answer:not(.is-answered) {
  cursor: pointer;
}
.answer:not(.is-answered):hover {
  background-color: #8ce200;
  border-color: #8ce200;
  color: #fff;
}
</style>
