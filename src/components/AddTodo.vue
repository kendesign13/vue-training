<template>

    <form id="form" @submit.prevent="onSubmit" class="todoFrame">
        <div class="todoBox">
            <input 
                class="form-control todoInput" 
                v-model="text" 
                :placeholder="placeholderText" 
                :class="{ 'placeholder-red': showError }" 
                @input="onInput" 
                type="text"
            >
        </div>

        <div>
            <button class="btn btn-add">Add Todo</button>
        </div>
    </form>
</template>


<script setup>
import { ref, defineEmits } from "vue";

const text = ref("");
const placeholderText = ref("Todo Text...");
const showError = ref(false);

const emit = defineEmits(["addTodo"]);

const onSubmit = () => {
    if (text.value.trim() === "") {
        placeholderText.value = "請輸入文字";
        showError.value = true;
        return;
    }
    const todo = {
        id: crypto.randomUUID(),
        text: text.value,
        complete: false
    };
    emit("addTodo", todo);
    text.value = "";
    placeholderText.value = "Todo Text...";
    showError.value = false;
};

const onInput = () => {
    if (showError.value) {
        placeholderText.value = "Todo Text...";
        showError.value = false;
    }
};
</script>

<style lang="scss">


</style>