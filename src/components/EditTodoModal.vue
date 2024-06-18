<template>
    <div class="modal" v-if="visible">
        <div class="modal-content">
            <label class="form-label label-title">Edit Todo</label>
            <input class="form-control mb-2" :class="{ 'input-error': isInputEmpty }" v-model="editedText"
                @focus="onFocus" @input="onInput" />
            <div class="form-footer">
                <button class="btn btn-save" @click="saveEdit">Save</button>
                <button class="btn btn-cancel" @click="closeModal">Cancel</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
    visible: Boolean,
    todo: Object,
});

const emits = defineEmits(['close', 'save']);

const editedText = ref('');
const isInputEmpty = ref(false);

watch(() => props.todo, (newTodo) => {
    if (newTodo) {
        editedText.value = newTodo.text;
        isInputEmpty.value = false; // Reset error state when a new todo is loaded
    }
}, { immediate: true });

const saveEdit = () => {
    if (editedText.value.trim() === "") {
        editedText.value = "Need write something...";
        isInputEmpty.value = true;
    } else {
        emits('save', { ...props.todo, text: editedText.value });
        closeModal();
    }
};

const onInput = () => {
    if (isInputEmpty.value && editedText.value !== 'Need write something...') {
        isInputEmpty.value = false;
    }
};

const onFocus = () => {
    if (editedText.value === 'Need write something...') {
        editedText.value = '';
        isInputEmpty.value = false;
    }
};

const closeModal = () => {
    emits('close');
};
</script>

<style scoped>

</style>
