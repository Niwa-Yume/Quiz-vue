<template>
    <div>


      <h1>{{ quiz.title }}</h1>



      <!-- question + choix -->
      <div v-if="quiz.questions[currentQuestionIndex]">
        <h2>{{quiz.questions[currentQuestionIndex].question}}</h2>
        <p>Question {{ currentQuestionIndex + 1 }}/{{ quiz.questions.length }}</p>


        <!-- bar de progrès -->
        <div class="progress-bar" style="margin-bottom: 15px">
          <div class="bar" :style="{ width: `${(currentQuestionIndex / quiz.questions.length) * 100}%` }"></div>
        </div>

        <!-- CHOIX REPONSE -->
        <div class="choices" style="margin-bottom: 15px">
          <!-- choix valeur réponse -->
          <div
            v-for="(choice, index) in quiz.questions[currentQuestionIndex].choices"
            :key="index"
            class="choice"
          >
            <input type="radio" :value="choice" v-model="choicesAnswer"  :id="index" :name="currentQuestionIndex" />
            <label :for="index">{{ choice }}</label>
          </div>
        </div>
      </div>

      <!-- Bouton validation si valeur pas vide et itération + 1 index -->
      <div>
        <!-- clique ajout de la fonction aussi -->
        <button
          v-if="currentQuestionIndex < quiz.questions.length"
          @click="nextQuestion();">
          Question suivante
        </button>

        <!-- message de succès ou d'échec si toutes les questions sont répondues -->
        <div v-if="currentQuestionIndex >= quiz.questions.length">
          <h2>Quiz terminé!</h2>
          <p>Votre score: {{ goodAnswer }}/{{ quiz.questions.length }}</p>
          <p>{{ goodAnswer >= quiz.minimum_score ? quiz.success_message : quiz.failure_message }}</p>
        </div>

      </div>


      <!-- message de succès ou d'échec -->
    </div>
</template>

<script setup>

import {ref} from "vue";

const choicesAnswer = ref("");
const goodAnswer = ref(0);
const progressbarCount = ref(0);
const currentQuestionIndex = ref(0);

const quiz = {
  "title": "Questionnaire sur les Films et Séries",
  "minimum_score": 4,
  "success_message": "Félicitations! Vous êtes un véritable cinéphile!",
  "failure_message": "Dommage! Vous devriez regarder plus de films et séries.",
  "questions": [
    {
      "question": "Dans quel film trouve-t-on le personnage de Jack Dawson?",
      "choices": ["Titanic", "Le Seigneur des Anneaux", "Inception", "Avatar"],
      "correct_answer": "Titanic"
    },
    {
      "question": "Quelle série met en scène le personnage de Walter White?",
      "choices": [
        "Breaking Bad",
        "Stranger Things",
        "Game of Thrones",
        "The Walking Dead"
      ],
      "correct_answer": "Breaking Bad"
    },
    {
      "question": "Dans quel film Harry Potter rencontre-t-il pour la première fois Lord Voldemort?",
      "choices": [
        "Harry Potter à l'école des sorciers",
        "Harry Potter et la Chambre des secrets",
        "Harry Potter et le Prisonnier d'Azkaban",
        "Harry Potter et la Coupe de feu"
      ],
      "correct_answer": "Harry Potter à l'école des sorciers"
    },
    {
      "question": "Quel est le nom de l'intelligence artificielle dans '2001: L'Odyssée de l'espace'?",
      "choices": ["HAL 9000", "Siri", "Cortana", "Jarvis"],
      "correct_answer": "HAL 9000"
    },
    {
      "question": "Qui joue le rôle principal dans la série 'Sherlock' de la BBC?",
      "choices": [
        "Benedict Cumberbatch",
        "David Tennant",
        "Matt Smith",
        "Tom Hiddleston"
      ],
      "correct_answer": "Benedict Cumberbatch"
    }
  ]
};


function nextQuestion() {
  // Vérifier si la réponse est correcte
  if (choicesAnswer.value === quiz.questions[currentQuestionIndex.value].correct_answer) {
    goodAnswer.value++;
  }

  // Passer à la question suivante
  currentQuestionIndex.value++;
  progressbarCount.value++;

  // Réinitialiser la sélection pour la prochaine question
  choicesAnswer.value = "";
}
</script>

<style scoped>
.progress-bar {
  width: 20%;
  height: 20px;
  background-color: #e0e0e0;
  border-radius: 10px;
}

.bar {
  height: 100%;
  background-color: #4c74af;
  transition: width 0.3s ease;
}
</style>