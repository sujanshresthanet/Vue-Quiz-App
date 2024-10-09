<template>
  <div class="card mb-4">
    <div class="card-body">
      <h4>{{ question.text }}</h4>
      <div v-for="(option, index) in question.options" :key="index" class="mb-2">
        <button 
          class="btn w-100"
          :class="getButtonClass(option)"
          @click="answerQuestion(option)"
          :disabled="showFeedback"
        >
          {{ option }}
        </button>
      </div>

      <!-- Correct answer feedback -->
      <div v-if="showFeedback" class="mt-3">
        <p class="text-success" v-if="selectedAnswer === question.correctAnswer">
          Correct! The answer is {{ question.correctAnswer }}.
        </p>
        <p class="text-danger" v-else>
          Wrong! The correct answer is {{ question.correctAnswer }}.
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['question', 'showFeedback', 'selectedAnswer'],
  methods: {
    answerQuestion(option) {
      this.$emit('answered', option);
    },
    getButtonClass(option) {
      if (!this.showFeedback) {
        return 'btn-outline-primary';
      }

      // Green for correct, red for incorrect
      if (option === this.question.correctAnswer) {
        return 'btn-success';
      } else if (option === this.selectedAnswer) {
        return 'btn-danger';
      } else {
        return 'btn-outline-secondary';
      }
    }
  }
}
</script>

<style scoped>
/* Optional styles */
</style>
