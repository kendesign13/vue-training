<template>
    <div class="modal" v-if="visible">
        <div class="modal-content">
            <label class="form-label label-title">Edit Todo</label>
            <input class="form-control mb-2" v-model="editedText" />
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

watch(() => props.todo, (newTodo) => {
    if (newTodo) {
        editedText.value = newTodo.text;
    }
}, { immediate: true });

const saveEdit = () => {
    emits('save', { ...props.todo, text: editedText.value });
};

const closeModal = () => {
    emits('close');
};
</script>

<style scoped></style>
