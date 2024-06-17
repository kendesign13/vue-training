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


.form-control {
    display: block;
    width: 100%;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.form-control:focus {
    color: #212529;
    background-color: #fff;
    border-color: #86b7fe;
    outline: 0;
    box-shadow: 0 0 0 .25rem rgba(13, 110, 253, .25);
}

.placeholder-red::placeholder {
    color: #dc3545;
}

.btn {
    display: inline-block;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    text-align: center;
    text-decoration: none;
    vertical-align: middle;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    user-select: none;
    background-color: transparent;
    border: 1px solid transparent;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    border-radius: 0.25rem;
    transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.todoFrame {
    display: flex;
    flex-flow: row wrap;
    gap: 10px;

    .todoBox {
        // width: 100%;
        flex:1 0 auto;
    }

    .todoInput {
        line-height: 1.25rem;
        font-size: 1rem;
        height: 40px;
        padding: .5rem;
        border-radius: 5px;

    }

    .btn-add {
        font-weight: 600;
        border: none;
        height: 40px;
        outline: none;
        color: var(--vt-c-white);
        background: rgb(0, 87, 209);
    }

    .btn-add:hover {
        background: rgb(20, 78, 159);
    }
}
</style>