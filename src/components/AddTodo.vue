<template>

    <form id="form" @submit.prevent="onSubmit" class="todoFrame">
        <div class="todoBox">
            <input class="form-control todoInput" v-model="text" type="text" placeholder="Todo Text...">
        </div>

        <div>
            <button class="btn btn-add">Add Todo</button>
        </div>
    </form>
</template>


<script setup>

import { ref, defineEmits } from "vue";

const text = ref("");

const emit = defineEmits(["addTodo"])

const onSubmit = () => {
    const todo = {
        id: crypto.randomUUID(),
        text: text.value,
        complete: false
    }
    emit("addTodo", todo);
    text.value = ""; // 清空输入框的内容
}
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