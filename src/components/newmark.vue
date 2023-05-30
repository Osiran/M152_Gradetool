<template>
    <div class="d-flex justify-content-between">
        <div class="col-9 m-1">
        <input type="text" class="form-control" @keyup.enter="addMark(subject)" v-model="newMark"
            placeholder="insert mark here:" />
        </div>

        <div class="col-2 ml-4">
        <button class="btn btn-primary m-1" type="button" @click="addMark(subject)">+</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

    const newMark = ref("");
    const emit = defineEmits(["add"])


    function addMark() {
        emit('add', newMark.value)
        newMark.value = "";
    }
</script>