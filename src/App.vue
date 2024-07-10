<template>
  <div>
    <h1>Notes</h1>
    <form @submit.prevent="addCourse">
      <input v-model="newCourseName" placeholder="Nouvelle matière" required>
      <div v-for="(note, index) in newCourseGrades" :key="index">
        <input type="number" v-model.number="newCourseGrades[index]" placeholder="Nouvelle note" required>
        <button type="button" @click="removeNewGrade(index)">Supprimer note</button>
      </div>
      <button type="button" class="primary" @click="addNewGrade">Ajouter une note</button>
      &nbsp;
      <button v-if="show" type="submit" class="primary">Ajouter la matière</button>
    </form>
    <table>
      <thead>
        <tr>
          <th>Matière</th>
          <th v-for="(header, index) in maxAssessments" :key="index">Contrôle Continu #{{ index + 1 }}</th>
          <th>Moyenne</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(course, courseIndex) in courses" :key="course.name">
          <td>{{ course.name }}</td>
          <td v-for="(assessment, index) in maxAssessments" :key="index">
            <span :style="{ color: course.assessments[index] && course.assessments[index].grade < 10 ? 'orange' : ''}">
              {{ course.assessments[index] ? course.assessments[index].grade : '' }}
            </span>
          </td>
          <td :style="{ color: courseAverage(course) < 10 ? 'red' : '' }">{{ courseAverage(course).toFixed(2) }}</td>
          <td><button @click="removeCourse(courseIndex)" class="secondary">Supprimer</button></td>
        </tr>
        <tr>
          <td colspan="100%">Moyenne générale</td>
          <td :style="{ color: overAverage < 10 ? 'red' : '' }">{{ overAverage.toFixed(2) }}</td>
        </tr>
        <tr>
          <td colspan="100%">{{ moyMessage }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue';

interface Assessment {
  grade: number;
}

interface Course {
  name: string;
  assessments: Assessment[];
}

const courses = ref<Course[]>([
  {
    name: "Vue.js & TypeScript",
    assessments: [
      { grade: 13 },
      { grade: 12 },
    ]
  },
  {
    name: "TypeScript & Nest.js",
    assessments: [
      { grade: 7 },
      { grade: 13 },
      { grade: 9 },
    ]
  }
]);

const newCourseName = ref('');
const newCourseGrades = ref<number[]>([]);
const show = ref(false);

const addNewGrade = () => {
  newCourseGrades.value.push(0);
  show.value = true;
};

const removeNewGrade = (index: number) => {
  newCourseGrades.value.splice(index, 1);
  if (newCourseGrades.value.length === 0) {
    show.value = false;
  }
};

const addCourse = () => {
  if (newCourseName.value && newCourseGrades.value.length) {
    courses.value.push({
      name: newCourseName.value,
      assessments: newCourseGrades.value.map(grade => ({ grade }))
    });
    newCourseName.value = '';
    newCourseGrades.value = [];
    show.value = false;
  }
};

const removeCourse = (index: number) => {
  courses.value.splice(index, 1);
};

const maxAssessments = computed(() => {
  return Math.max(...courses.value.map(course => course.assessments.length));
});

const courseAverage = (course: Course) => {
  const sum = course.assessments.reduce((acc, assessment) => acc + assessment.grade, 0);
  return sum / course.assessments.length;
};

const overAverage = computed(() => {
  const totalSum = courses.value.reduce((acc, course) => acc + courseAverage(course), 0);
  return totalSum / courses.value.length;
});

const moyMessage = computed(() => {
  const avg = overAverage.value;
  if (avg < 5) {
    return "Des efforts à fournir afin de pouvoir valider l'année.";
  } else if (avg < 10) {
    return "Il y a des progrès, mais il reste encore du travail pour atteindre la moyenne.";
  } else if (avg < 15) {
    return "Bon travail, mais il est possible d'améliorer encore davantage.";
  } else {
    return "Excellent travail, continuez ainsi !";
  }
});
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid black;
  padding: 8px;
  text-align: left;
}

button {
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

.primary {
  background-color: rgb(24, 106, 247);
  color: white;
}

.primary:hover {
  background-color: rgb(24, 106, 247, 0.8);
}

.secondary {
  background-color: rgb(247, 24, 24);
  color: white;
}

.secondary:hover {
  background-color: rgb(247, 24, 24, 0.8);
}
</style>
