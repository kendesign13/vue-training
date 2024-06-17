<script setup>
// import { RouterLink, RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue';
import AddTodo from './components/AddTodo.vue';
import TodoList from './components/TodoList.vue';
import { ref } from "vue"


const todos = ref([
  // {
  //   id: 1,
  //   text: 'Test'
  // }

]);

const handleAddTodo = (todo) => {
  todos.value.push(todo);
}

const handleDeleteTodo = (todoId) => {
  todos.value = todos.value.filter((todo) => todo.id !== todoId)
}

const handleCompleteTodo = (todoId) => {
  todos.value = todos.value.map((todo) => todo.id === todoId ? { ...todo, complete: true } : todo)
}

</script>


<template>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header> -->

  <!-- <RouterView /> -->

  <div class="card">
    <AddTodo @add-todo="handleAddTodo" />
    <TodoList @delete-todo="handleDeleteTodo" @complete-todo="handleCompleteTodo" :todos="todos" />
  </div>

  <!-- <div class="test-scss">
    SCSS Test
  </div> -->


</template>

<style lang="scss">
.test-scss {
  // color: red;

  .nested {
    color: blue;
  }
}

.card {
  max-width: 800px;
  background-color: var(--vt-c-white);
  padding: 1rem;
  border: 1px solid var(--vt-c-text-dark-2);
  border-radius: .5rem;
  margin: 10% auto;

  transition: all .35s;
  box-shadow: 0px 20px 15px -10px rgba(55, 62, 85, 0.35), 0px 10px 15px -5px rgba(49, 90, 121, 0.8);
}
</style>


<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
