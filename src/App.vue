<template>
  <div class="container mt-5">
    <div class="text-center">
      <h1 class="mb-4">Vue.js Quiz App</h1>
    </div>

    <!-- Quiz section -->
    <div v-if="currentQuestionIndex < questions.length">
      <h5>Question {{ currentQuestionIndex + 1 }} of {{ questions.length }}</h5>
      <quiz-question
        :question="questions[currentQuestionIndex]"
        :showFeedback="showFeedback"
        :selectedAnswer="selectedAnswer"
        @answered="handleAnswer"
      />
      <div v-if="showFeedback" class="mt-3 text-center">
        <div class="d-flex justify-content-center gap-2">
            <button class="btn btn-primary" @click="nextQuestion">Next</button>
            <button class="btn btn-danger" @click="finishQuiz">Finish Quiz</button>
        </div>
      </div>
    </div>

    <!-- Summary section -->
    <div v-else class="text-center">
      <h2>Quiz Completed!</h2>
      <p>Your Score: <strong>{{ score }}</strong> out of {{ questions.length }} ({{ correctPercent }}% correct)</p>
      <p>Wrong answers: {{ wrongPercent }}%</p>

      <div class="card mt-4">
        <div class="card-body">
          <h4>Summary</h4>
          <ul class="list-group">
            <li v-for="(question, index) in questions" :key="index" class="list-group-item">
              <h5>{{ index + 1 }}. {{ question.text }}</h5>
              <div class="options">
                <div
                  v-for="(option, idx) in question.options"
                  :key="idx"
                  :class="{
                    'correct-answer': option === question.correctAnswer,
                    'user-answer': option === question.selectedAnswer && option !== question.correctAnswer,
                    'text-danger': option === question.selectedAnswer && option !== question.correctAnswer,
                    'text-success': option === question.correctAnswer && option === question.selectedAnswer
                  }"
                >
                  {{ option }}
                </div>
              </div>
              <div v-if="question.selectedAnswer" class="mt-2">
                <strong>Your answer:</strong>
                <span class="text-danger">{{ question.selectedAnswer }}</span>
                <br />
                <strong>Correct answer:</strong>
                <span class="text-success">{{ question.correctAnswer }}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>

      <!-- Restart Quiz Button -->
      <button class="btn btn-secondary mt-4" @click="restartQuiz">Restart Quiz</button>
    </div>
  </div>
</template>

<script>
import QuizQuestion from './components/QuizQuestion.vue';

export default {
  components: {
    QuizQuestion
  },
  data() {
    return {
      currentQuestionIndex: 0,
      score: 0,
      selectedAnswer: '',
      showFeedback: false,
      questions: [
        {
          text: "What is Vue.js?",
          options: ["A front-end framework", "A backend framework", "A CSS library", "A database"],
          correctAnswer: "A front-end framework",
          selectedAnswer: ""
        },
        {
          text: "What is a Vue instance?",
          options: ["An HTML element", "A Vue component", "A root Vue object", "A JavaScript class"],
          correctAnswer: "A root Vue object",
          selectedAnswer: ""
        },
        {
          text: "Which of the following is used to create a Vue component?",
          options: ["Vue.extend()", "Vue.createComponent()", "Vue.component()", "Vue.factory()"],
          correctAnswer: "Vue.component()",
          selectedAnswer: ""
        },
        {
          text: "What directive is used to display data in Vue?",
          options: ["v-bind", "v-show", "v-if", "v-model"],
          correctAnswer: "v-bind",
          selectedAnswer: ""
        },
        {
          text: "How do you bind a class to an element in Vue?",
          options: ["v-class", "class-bind", "v-bind:class", "bind:class"],
          correctAnswer: "v-bind:class",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the Vue Router?",
          options: ["State management", "Routing in a single-page application", "Data fetching", "CSS styling"],
          correctAnswer: "Routing in a single-page application",
          selectedAnswer: ""
        },
        {
          text: "Which lifecycle hook is called after the component has been mounted?",
          options: ["created", "mounted", "updated", "destroyed"],
          correctAnswer: "mounted",
          selectedAnswer: ""
        },
        {
          text: "What is Vuex used for?",
          options: ["Routing", "State management", "Creating components", "Fetching data"],
          correctAnswer: "State management",
          selectedAnswer: ""
        },
        {
          text: "What does v-if do in Vue?",
          options: ["Adds a class", "Conditionally renders an element", "Binds data", "Manages state"],
          correctAnswer: "Conditionally renders an element",
          selectedAnswer: ""
        },
        {
          text: "Which of the following is a valid way to define a Vue component?",
          options: ["const app = new Vue()", "Vue.component('my-component', {})", "Vue.createComponent('my-component', {})", "Vue.component()"],
          correctAnswer: "Vue.component('my-component', {})",
          selectedAnswer: ""
        },
        {
          text: "What does the v-model directive do?",
          options: ["Bind data to an input element", "Conditionally render elements", "Add a class", "Bind a CSS style"],
          correctAnswer: "Bind data to an input element",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the key attribute in Vue lists?",
          options: ["To uniquely identify list items", "To define styles", "To bind data", "To manage states"],
          correctAnswer: "To uniquely identify list items",
          selectedAnswer: ""
        },
        {
          text: "Which of the following is true about Vue's reactivity system?",
          options: ["It uses a virtual DOM", "It doesn't track changes", "It is synchronous", "It is only for data binding"],
          correctAnswer: "It uses a virtual DOM",
          selectedAnswer: ""
        },
        {
          text: "What is a computed property in Vue?",
          options: ["A function that returns a value", "A property that is reactive", "A method for rendering templates", "A way to manage state"],
          correctAnswer: "A property that is reactive",
          selectedAnswer: ""
        },
        {
          text: "How can you pass data to a child component in Vue?",
          options: ["Using props", "Using emit", "Using events", "Using data"],
          correctAnswer: "Using props",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the $emit method?",
          options: ["To send data from parent to child", "To trigger an event in the parent component", "To define a computed property", "To access data in a component"],
          correctAnswer: "To trigger an event in the parent component",
          selectedAnswer: ""
        },
        {
          text: "Which method is used to update the state in Vuex?",
          options: ["actions", "getters", "mutations", "modules"],
          correctAnswer: "mutations",
          selectedAnswer: ""
        },
        {
          text: "What is the Vue CLI used for?",
          options: ["Managing components", "Building Vue applications", "Routing", "State management"],
          correctAnswer: "Building Vue applications",
          selectedAnswer: ""
        },
        {
          text: "How do you create a Vue instance?",
          options: ["new Vue()", "Vue.create()", "Vue.init()", "createVue()"],
          correctAnswer: "new Vue()",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the created lifecycle hook?",
          options: ["To render the component", "To initialize data", "To update the DOM", "To destroy the component"],
          correctAnswer: "To initialize data",
          selectedAnswer: ""
        },
        {
          text: "What does the v-for directive do?",
          options: ["Iterates over an array", "Binds data", "Conditionally renders an element", "Adds a class"],
          correctAnswer: "Iterates over an array",
          selectedAnswer: ""
        },
        {
          text: "What is a Vue directive?",
          options: ["A special token in the markup", "A JavaScript function", "A CSS style", "A data model"],
          correctAnswer: "A special token in the markup",
          selectedAnswer: ""
        },
        {
          text: "Which of the following is not a valid Vue directive?",
          options: ["v-if", "v-show", "v-class", "v-model"],
          correctAnswer: "v-class",
          selectedAnswer: ""
        },
        {
          text: "What does the watch property do in Vue?",
          options: ["Watches for changes in data", "Renders templates", "Defines computed properties", "Manages state"],
          correctAnswer: "Watches for changes in data",
          selectedAnswer: ""
        },
        {
          text: "How can you include external libraries in a Vue project?",
          options: ["Using npm", "Including in HTML", "Both a and b", "None of the above"],
          correctAnswer: "Both a and b",
          selectedAnswer: ""
        },
        {
          text: "What is the role of the template in Vue?",
          options: ["Styling", "Rendering HTML", "Managing state", "Fetching data"],
          correctAnswer: "Rendering HTML",
          selectedAnswer: ""
        },
        {
          text: "How do you handle events in Vue?",
          options: ["Using v-on", "Using event listeners", "Using methods", "Using directives"],
          correctAnswer: "Using v-on",
          selectedAnswer: ""
        },
        {
          text: "Which method is used to fetch data from an API in Vue?",
          options: ["fetchData()", "axios()", "getData()", "httpClient()"],
          correctAnswer: "axios()",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the mounted lifecycle hook?",
          options: ["To fetch data", "To manipulate the DOM", "To set initial data", "To destroy the component"],
          correctAnswer: "To manipulate the DOM",
          selectedAnswer: ""
        },
        {
          text: "Which property allows you to bind inline styles in Vue?",
          options: ["v-style", "v-bind:style", "style-bind", "v-inline"],
          correctAnswer: "v-bind:style",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the $nextTick method?",
          options: ["To access the DOM after updates", "To handle events", "To define data properties", "To manage state"],
          correctAnswer: "To access the DOM after updates",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of Vue Devtools?",
          options: ["Debugging Vue applications", "Creating components", "Building applications", "Managing state"],
          correctAnswer: "Debugging Vue applications",
          selectedAnswer: ""
        },
        {
          text: "How do you define a filter in Vue?",
          options: ["Vue.filter()", "filters: {}", "v-filter", "defineFilter()"],
          correctAnswer: "Vue.filter()",
          selectedAnswer: ""
        },
        {
          text: "What is a slot in Vue?",
          options: ["A placeholder for content", "A method for data binding", "A lifecycle hook", "A directive"],
          correctAnswer: "A placeholder for content",
          selectedAnswer: ""
        },
        {
          text: "How do you create a dynamic class binding in Vue?",
          options: ["v-bind:class", "v-class", "dynamic-class", "class:bind"],
          correctAnswer: "v-bind:class",
          selectedAnswer: ""
        },
        {
          text: "What does the v-show directive do?",
          options: ["Hides elements conditionally", "Binds data", "Displays data", "Adds a class"],
          correctAnswer: "Hides elements conditionally",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the Vuex store?",
          options: ["To manage application state", "To define components", "To handle routing", "To fetch data"],
          correctAnswer: "To manage application state",
          selectedAnswer: ""
        },
        {
          text: "Which of the following is a way to handle form input in Vue?",
          options: ["v-model", "v-bind", "v-on", "v-if"],
          correctAnswer: "v-model",
          selectedAnswer: ""
        },
        {
          text: "How can you implement a global mixin in Vue?",
          options: ["Vue.mixin()", "globalMixin()", "Vue.extend()", "Vue.component()"],
          correctAnswer: "Vue.mixin()",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the v-bind directive?",
          options: ["To bind data to HTML attributes", "To create a Vue component", "To manage state", "To handle events"],
          correctAnswer: "To bind data to HTML attributes",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the key modifier in Vue?",
          options: ["To handle keyboard events", "To manage state", "To define props", "To set computed properties"],
          correctAnswer: "To handle keyboard events",
          selectedAnswer: ""
        },
        {
          text: "How can you access a child component's method from a parent component?",
          options: ["Using refs", "Using props", "Using emit", "Using slots"],
          correctAnswer: "Using refs",
          selectedAnswer: ""
        },
        {
          text: "Which of the following allows you to create reusable Vue components?",
          options: ["Mixins", "Slots", "Filters", "All of the above"],
          correctAnswer: "All of the above",
          selectedAnswer: ""
        },
        {
          text: "What does the watch property return in Vue?",
          options: ["The current state", "The previous state", "The next state", "An array of states"],
          correctAnswer: "The previous state",
          selectedAnswer: ""
        },
        {
          text: "How do you install Vue Router?",
          options: ["npm install vue-router", "yarn add vue-router", "Both a and b", "None of the above"],
          correctAnswer: "Both a and b",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the data() function in Vue components?",
          options: ["To define data properties", "To create computed properties", "To manage events", "To create methods"],
          correctAnswer: "To define data properties",
          selectedAnswer: ""
        },
        {
          text: "How do you access props in a Vue component?",
          options: ["this.props", "this.$props", "props", "this.$data"],
          correctAnswer: "this.$props",
          selectedAnswer: ""
        },
        {
          text: "Which of the following is used to import a Vue component?",
          options: ["import Component from './Component.vue'", "require('./Component.vue')", "import './Component.vue'", "All of the above"],
          correctAnswer: "All of the above",
          selectedAnswer: ""
        },
        {
          text: "What is the purpose of the beforeDestroy lifecycle hook?",
          options: ["To initialize data", "To clean up resources", "To render the component", "To update the DOM"],
          correctAnswer: "To clean up resources",
          selectedAnswer: ""
        },
        {
          text: "Which of the following is a valid way to define computed properties?",
          options: ["computed: { }", "data: { }", "methods: { }", "watch: { }"],
          correctAnswer: "computed: { }",
          selectedAnswer: ""
        },
        {
          text: "What is the use of the v-pre directive?",
          options: ["To skip compilation for this element", "To bind data", "To manage state", "To define props"],
          correctAnswer: "To skip compilation for this element",
          selectedAnswer: ""
        }
 ]
    }
  },
  computed: {
    correctPercent() {
      return ((this.score / this.questions.length) * 100).toFixed(2);
    },
    wrongPercent() {
      const wrongAnswers = this.questions.length - this.score;
      return ((wrongAnswers / this.questions.length) * 100).toFixed(2);
    }
  },
  mounted() {
    // Load quiz state from localStorage if available
    this.loadQuizState();
  },
  methods: {
    handleAnswer(answer) {
      const currentQuestion = this.questions[this.currentQuestionIndex];
      currentQuestion.selectedAnswer = answer;
      this.selectedAnswer = answer;
      this.showFeedback = true;

      // Check if the selected answer is correct
      if (answer === currentQuestion.correctAnswer) {
        this.score++;
      }

      // Save state in localStorage
      this.saveQuizState();
    },
    nextQuestion() {
      this.currentQuestionIndex++;
      this.selectedAnswer = '';
      this.showFeedback = false;

      // Clear feedback for the next question
      this.saveQuizState();
    },
    finishQuiz() {
      // Finish the quiz and go to the summary
      this.currentQuestionIndex = this.questions.length; // Set to length to show summary
      this.saveQuizState();
    },
    saveQuizState() {
      const quizState = {
        currentQuestionIndex: this.currentQuestionIndex,
        score: this.score,
        questions: this.questions
      };
      localStorage.setItem('vueQuizState', JSON.stringify(quizState));
    },
    loadQuizState() {
      const savedState = localStorage.getItem('vueQuizState');
      if (savedState) {
        const quizState = JSON.parse(savedState);
        this.currentQuestionIndex = quizState.currentQuestionIndex;
        this.score = quizState.score;
        this.questions = quizState.questions;
      }
    },
    restartQuiz() {
      this.currentQuestionIndex = 0;
      this.score = 0;
      this.selectedAnswer = '';
      this.showFeedback = false;

      // Clear each question's selected answer
      this.questions.forEach(question => (question.selectedAnswer = ''));

      // Clear state from localStorage
      localStorage.removeItem('vueQuizState');
    }
  },
  watch: {
    currentQuestionIndex(newIndex) {
      if (newIndex >= this.questions.length) {
        localStorage.removeItem('vueQuizState');
      }
    }
  }
}
</script>

<style scoped>
.correct-answer {
  background-color: #d4edda; /* Green background for correct answers */
}
.user-answer {
  background-color: #f8d7da; /* Red background for wrong user answers */
}
.options div {
  padding: 5px 10px;
  border-radius: 5px;
  margin-bottom: 5px;
}
</style>