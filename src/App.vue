<template>
    <div>
      <h1>{{ quiz.title }}</h1>
      <!-- bar de progrès -->
      <div class="progress-bar">

      </div>


      <!-- question + choix -->
      <div v-if="quiz.questions[currentQuestionIndex]">
        <h2>{{quiz.questions[currentQuestionIndex].question}}</h2>
        <p>Question {{ currentQuestionIndex + 1 }}/{{ quiz.questions.length }}</p>


        <!-- CHOIX REPONSE -->
        <div class="choices">
          <!-- choix valeur réponse -->
          <div
            v-for="(choice, index) in quiz.questions[currentQuestionIndex].choices"
            :key="index"
            class="choice"
          >
            <input type="radio" :id="index" :name="currentQuestionIndex" />
            <label :for="index">{{ choice }}</label>
          </div>
        </div>
      </div>

      <!-- Bouton validation si valeur pas vide et itération + 1 index -->
      <div>
        <button
          @click="currentQuestionIndex.value++"
        >Question suivante</button>


      </div>


      <!-- message de succès ou d'échec -->
    </div>
</template>

<script setup>

import {ref} from "vue";

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
</script>

<style scoped>
</style>