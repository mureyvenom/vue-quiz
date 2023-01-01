<script lang="ts">
export default {
  name: 'ResultComponent',
  props: {
    results: {
      type: Array<{
        min: number;
        max: number;
        title: string;
        desc: string;
      }>,
      default: [],
    },
    totalCorrect: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    resultIndex() {
      let index = 0;

      this.results?.forEach((e, i) => {
        if (e.min <= this.totalCorrect && e.max >= this.totalCorrect) {
          index = i;
        }
      });

      return index;
    },
  },
};
</script>

<template>
  <div class="w-full">
    <div class="w-full p-5 text-3xl font-bold text-center text-white bg-[#12cbc4] box-border">
      {{ results[resultIndex].title }}
    </div>
    <div
      class="w-full p-5 text-lg bg-white text-center transition-all duration-300 border-[1px] border-[#8e959f]"
    >
      {{ results[resultIndex].desc }}
    </div>
  </div>
</template>
