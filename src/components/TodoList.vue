<template>
    <ul v-if="todos.length > 0" class="todoListFrame">
        <li v-for="todo in todos" :key="todo.id" class="todoList">
            <button class="btn btn-delete" @click="deleteTodo(todo.id)">
                <span class="material-symbols-outlined">close</span>
            </button>
            <button class="btn btn-complete" @click="completeTodo(todo)">
                <span class="material-symbols-outlined">check</span>
            </button>
            <button class="btn btn-edit" @click="showEditModal(todo)">
                <span class="material-symbols-outlined">edit</span>
            </button>
            <p class="todo" :class="{ 'complete': todo.complete }">{{ todo.text }}</p>
        </li>
    </ul>
    <p v-else class="tips">No Todos found</p>
    <EditTodoModal :visible="isEditModalVisible" :todo="currentTodo" @close="hideEditModal" @save="updateTodo" />
</template>

<script setup>
import { ref } from 'vue';
import EditTodoModal from './EditTodoModal.vue';

const props = defineProps({
    todos: {
        type: Array,
        required: true
    }
});

const emit = defineEmits(['deleteTodo', 'completeTodo', 'updateTodo']);

const isEditModalVisible = ref(false);
const currentTodo = ref(null);

const deleteTodo = (todoId) => {
    emit('deleteTodo', todoId);
};

const completeTodo = (todo) => {
    todo.complete = !todo.complete;
    emit('completeTodo', todo);
};

const showEditModal = (todo) => {
    currentTodo.value = todo;
    isEditModalVisible.value = true;
};

const hideEditModal = () => {
    isEditModalVisible.value = false;
};

const updateTodo = (updatedTodo) => {
    // 在這裡找到對應的待辦事項並更新其文本
    const index = props.todos.findIndex(todo => todo.id === updatedTodo.id);
    if (index !== -1) {
        props.todos[index].text = updatedTodo.text;
    }
    emit('updateTodo', updatedTodo);
    hideEditModal();
};
</script>

<style lang="scss"></style>
