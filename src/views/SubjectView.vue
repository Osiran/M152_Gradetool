<template>
  <div class="wrap main-body">
    <ul class="list-group mb-4" v-for="subject in subjects">
      <li class="list-group-item subject-body">
        <div class="subject-title text-wrap m-1">
          <h3>{{ subject.name }}</h3>
        </div>

        <hr class="rounded">

        <div class="m-1 input-group d-flex justify-content-between">
          <h4 class="m-1 title-center text-center">Average Ø: {{ getAverage(subject.Grades) }}</h4>
        </div>

        <NewGrade @add="addGrade(subject, $event)"></NewGrade>

        <hr class="rounded">

        <ul class="list-group" v-for="Grade in subject.Grades">

          <div class="input-group d-flex justify-content-between">
            <div class="col-9 m-1">
              <input readonly type="text" class="form-control" :value="Grade.Grade">
            </div>

            <div class="col-2 ml-4">
              <button class="btn btn-danger m-1" type="button" @click="removeGrade(subject, Grade.id)">X</button>
            </div>
          </div>

        </ul>
      </li>
    </ul>
  </div>

  <div class="wrap input-group subject-add fixed-bottom">

    <div class="m-1 input-group d-flex justify-content-between">
      <h4 class="m-1 title-center text-center">Average Ø: {{ totalAverage(subjects) }}</h4>
    </div>

    <input type="text" class="form-control m-1" @keyup.enter="addSubject(subjects)" v-model="newSubject"
      placeholder="Add Subject:" />
    <button class="btn btn-primary m-1" type="button" @click="addSubject(subjects)">+</button>
  </div>
</template>

<script setup>
// @ is an alias to /src
import { ref } from 'vue'
import NewGrade from '../components/newGrade'

const newSubject = ref("");
const subjects = ref([{
  id: 1,
  name: "M152",
  Grades: [
    { id: 1, Grade: 3 },
    { id: 2, Grade: 5 },
    { id: 3, Grade: 6 }
  ]
},
{ id: 2, name: "M151", Grades: [] },
{ id: 3, name: "M152", Grades: [] },
{ id: 4, name: "NWS", Grades: [] }]);

function addSubject(subjectList) {
  var nextID = incrementNextID(subjectList);

  subjects.value.push({
    id: nextID,
    name: newSubject.value,
    Grades: []
  });

  newSubject.value = "";
}

function addGrade(subject, grade) {
  if (!isValidGrade(grade)) {
    alert("Please enter a valid Grade between 1 and 6.")
    return;
  }
  subject.Grades.push({ id: incrementNextID(subject.Grades), Grade: grade })

  grade = "";
}

function removeGrade(subject, GradeID) {
  var index = subject.Grades.findIndex(function (x) {
    return x.id === GradeID;
  })
  if (index !== -1) { subject.Grades.splice(index, 1); }
}

function incrementNextID(arr) {
  if (arr.length <= 0) { return 1; }

  const idList = arr.map(x => {
    return x.id;
  });

  var nextID = Math.max(...idList) + 1;

  return nextID;
}

function getAverage(arr) {
  if (arr.length <= 0) { return "-"; }

  let GradeTotal = 0;
  arr.forEach(x => {
    GradeTotal += Number(x.Grade);
  });

  console.log(GradeTotal);
  GradeTotal = GradeTotal / arr.length
  return Math.round((GradeTotal + Number.EPSILON) * 100) / 100

}

function totalAverage(arr) {
  let total = 0;
  let empty = 0;

  arr.forEach(x => {
    if (x.Grades.length > 0) { total += getAverage(x.Grades) } else { empty += 1 }
  });
  if (total <= 0) { return "-" }

  total = total / (this.subjects.length - empty);

  return Math.round(total * 2) / 2;
}

function isValidGrade(str) {
  if (typeof str !== 'string') { return false; }

  let num = Number(str);

  if (!isNaN(num) && num > 0 && num <= 6) { return true } else { return false; }
}

</script>

