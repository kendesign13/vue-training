<template>
    <ul v-if="todos.length > 0" class="todoListFrame">
        <li v-for="todo in todos" :key="todo.id" class="todoList">
            <button class="btn-delete" @click="deleteTodo(todo.id)"><span class="material-symbols-outlined">
                    close
                </span></button>
            <button class="btn-complete" @click="completeTodo(todo.id)"><span class="material-symbols-outlined">
                    check
                </span></button>
            <!-- <p class="list-content">{{ todo.text }}</p> -->
            <p class="todo" :class="{ 'complete': todo.complete }">{{ todo.text }}</p>
        </li>
    </ul>
    <p v-else class="tips">No Todos found</p>
</template>

<script setup>

import { defineProps, defineEmits } from 'vue'

defineProps({
    todos: {
        type: Array,
    }
})

const emit = defineEmits(['deleteTodo', 'completeTodo'])

const deleteTodo = (todoId) => {
    emit('deleteTodo', todoId)
}


const completeTodo = (todoId) => {
    emit('completeTodo', todoId)
}

</script>


<style lang="scss">
.test-scss {
    color: green;

    .nested {
        color: blue;
    }
}

.bg-test {
    background: rgba(0, 235, 255, .75);
}

.todoListFrame {
    list-style: none;
    padding: 0;
    display: flex;
    flex-flow: column wrap;
    height: auto;
    max-height: 100%;
    transition: all .35s;

    .todoList {
        padding: 1rem .5rem;
        display: flex;
        flex-flow: row wrap;
        align-items: center;
        gap: .5rem;
        border-bottom: 1px solid var(--vt-c-text-dark-2);

        .todo {
            line-height: 1;
            font-size: 1rem;
            padding: 0 .25rem;
            color: var(--vt-c-indigo);

            &.complete {
                text-decoration-line: line-through;
            }
        }


        button {
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            width: 30px;
            height: 30px;
            color: var(--vt-c-white);
            // padding: .15rem;
            border: 0px;
            border-radius: 1000px;
            font-size: 2rem;
            font-weight: bold;
            transition: all .35s;
        }

        .btn-delete {
            outline: none;
            box-shadow: inset 2px 2px 3px 0px rgba(255, 162, 0, 0.638);
            background: rgba(255, 42, 43, 1);
            background: linear-gradient(135deg, rgba(255, 6, 6, 1) 0%, rgba(143, 0, 0, 1) 100%);
        }

        .btn-delete:hover {
            box-shadow: inset 2px 2px 3px 0px rgba(135, 0, 0, 0.85);
            background: rgb(255, 42, 43);
            background: linear-gradient(315deg, rgba(255, 6, 6, 1) 0%, rgba(143, 0, 0, 1) 100%);
        }

        .btn-complete {
            outline: none;
            box-shadow: inset 2px 2px 3px 0px rgba(0, 235, 255, .75);
            background: rgba(255, 42, 43, 1);
            background: linear-gradient(135deg, rgb(0, 202, 162) 0%, rgb(0, 136, 255) 100%);
        }


        .btn-complete:hover {
            outline: none;
            box-shadow: inset 2px 2px 3px 0px rgba(0, 90, 100, 0.75);
            background: rgb(0, 136, 255);
            background: linear-gradient(315deg, rgb(0, 202, 162) 0%, rgb(0, 136, 255) 100%);
        }


        .list-content {
            color: var(--vt-c-black-soft);
            font-size: 1rem;
            font-weight: 600;
            line-height: normal;
        }
    }
}

.tips {
    color: var(--vt-c-divider-dark-2);
}
</style>
