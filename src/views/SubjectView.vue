<template>
  <div class="wrap main-body">
    <ul class="list-group mb-4" v-for="subject in subjects">
      <li class="list-group-item subject-body">
        <div class="subject-title text-wrap m-1">
          <h3>{{ subject.name }}</h3>
        </div>

        <hr class="rounded">

        <div class="m-1 input-group d-flex justify-content-between">
          <h4 class="m-1 title-center text-center">Average Ø: {{ getAverage(subject.marks) }}</h4>

          <!-- <div class="input-group-prepend">
            <span class="input-group-text m-1" id="basic-addon1">Average</span>
          </div>
          <input readonly type="text" class="form-control m-1" :value="getAverage(subject.marks)"> -->
        </div>

        <Newmark @add="addMark(subject, $event)"></Newmark>

        <hr class="rounded">

        <ul class="list-group" v-for="mark in subject.marks">

          <div class="input-group d-flex justify-content-between">
            <div class="col-9 m-1">
              <input readonly type="text" class="form-control" :value="mark.mark">
            </div>

            <div class="col-2 ml-4">
              <button class="btn btn-danger m-1" type="button" @click="removeMark(subject, mark.id)">X</button>
            </div>
          </div>

        </ul>
      </li>
    </ul>
  </div>

  <div class="wrap input-group subject-add fixed-bottom">

    <div class="m-1 input-group d-flex justify-content-between">
      <h4 class="m-1 title-center text-center">Average Ø: {{ totalAverage(subjects) }}</h4>
      <!-- <input readonly type="text" class="form-control m-1" :value="totalAverage(subjects)"> -->
    </div>

    <input type="text" class="form-control m-1" @keyup.enter="addSubject(subjects)" v-model="newSubject"
      placeholder="Add Subject:" />
    <button class="btn btn-primary m-1" type="button" @click="addSubject(subjects)">+</button>
  </div>

</template>

<script setup>
// @ is an alias to /src
import { ref } from 'vue'
import Newmark from '../components/newmark'

const newSubject = ref("");
const subjects = ref([{
  id: 1,
  name: "M152",
  marks: [
    { id: 1, mark: 3 },
    { id: 2, mark: 5 },
    { id: 3, mark: 6 }
  ]
}, 
{ id: 2, name: "M151", marks: [] },
{ id: 3, name: "M306", marks: [] },
{ id: 4, name: "NWS", marks: [] },
{ id: 5, name: "SPK", marks: [] },
{ id: 6, name: "M153", marks: [] },
{ id: 7, name: "GES", marks: [] },
{ id: 8, name: "SPO", marks: [] },
{ id: 9, name: "WUR", marks: [] }]);

// , { id: 2, name: "M151", marks: [] },
//   { id: 3, name: "M306", marks: [] },
//   { id: 4, name: "M152", marks: [] },
//   { id: 5, name: "M152", marks: [] },
//   { id: 6, name: "M152", marks: [] },
//   { id: 7, name: "M152", marks: [] },
//   { id: 8, name: "M152", marks: [] }

function addSubject(subjectList) {
  var nextID = incrementNextID(subjectList);

  subjects.value.push({
    id: nextID,
    name: newSubject.value,
    marks: []
  });

  newSubject.value = "";
}

function addMark(subject, grade) {
  if (!isValidMark(grade)) {
    alert("Please enter a valid mark between 1 and 6.")
    return;
  }
  subject.marks.push({ id: incrementNextID(subject.marks), mark: grade })

  grade = "";
}

function removeMark(subject, markID) {
  var index = subject.marks.findIndex(function (x) {
    return x.id === markID;
  })
  if (index !== -1) { subject.marks.splice(index, 1); }
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

  let markTotal = 0;
  arr.forEach(x => {
    markTotal += Number(x.mark);
  });

  console.log(markTotal);
  markTotal = markTotal / arr.length
  return Math.round((markTotal + Number.EPSILON) * 100) / 100

}

function totalAverage(arr) {
  let total = 0;
  let empty = 0;

  arr.forEach(x => {
    if (x.marks.length > 0) { total += getAverage(x.marks) } else { empty += 1 }
  });
  if (total <= 0) { return "-" }

  total = total / (this.subjects.length - empty);

  return Math.round(total * 2) / 2;
}

function isValidMark(str) {
  if (typeof str !== 'string') { return false; }

  let num = Number(str);

  if (!isNaN(num) && num > 0 && num <= 6) { return true } else { return false; }
}

</script>

