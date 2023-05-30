<template>
    <div class="d-flex justify-content-between">
        <div class="col-9 m-1">
            <input type="text" class="form-control" @keyup.enter="addGrade(subject)" v-model="newGrade"
                placeholder="add Grade" />
        </div>

        <div class="col-2 ml-4">
            <button class="btn btn-primary m-1" type="button" @click="addGrade(subject)">+</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const newGrade = ref("");
const emit = defineEmits(["add"])


function addGrade() {
    emit('add', newGrade.value)
    newGrade.value = "";
}
</script>