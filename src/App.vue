<template>
  <div id="app">
    <h1>{{ msg }}</h1>

    <form v-on:submit.prevent="submitHandler">
      <input v-model="newTodoValue" type="text" placeholder="Add Todo" required>
      <button type="submit">Add Todo</button>
    </form>

    <h2>Open Todos <span class="counter">{{ undoneTodoAmount }}</span></h2>

    <TodoList v-bind:todos="undoneTodos" v-on:toggleDone="toggleDone" />

    <h2>Done <span class="counter">{{ doneTodoAmount }}</span></h2>

    <TodoList v-bind:todos="doneTodos" v-on:toggleDone="toggleDone" />
  </div>
</template>

<script>
import TodoList from './components/TodoList'

let i = 1;

export default {
  name: 'app',
  components: {
    TodoList,
  },
  data() {
    return {
      msg: 'My Todo App',
      newTodoValue: '',
      todos: [
        {
          id: i++,
          title: 'My first todo',
          done: false,
        },
        {
          id: i++,
          title: 'My second todo',
          done: false,
        }
      ]
    };
  },
  methods: {
    submitHandler() {
      this.todos.push({
        id: i++,
        title: this.newTodoValue,
        done: false,
      })
      this.newTodoValue = '';
    },
    toggleDone(todo) {
      this.updateTodo({
        action: (todo.done) ? 'undone' : 'done',
        todo,
      })
    },
    updateTodo(obj) {
      switch (obj.action) {
        case 'undone':
          obj.todo.done = false;
          break;
        case 'done':
          obj.todo.done = true;
          break;
        default:
          break;
      }
    }
  },
  computed: {
    undoneTodos() {
      return this.todos.filter(todo => !todo.done)
    },
    doneTodos() {
      return this.todos.filter(todo => todo.done)
    },
    undoneTodoAmount() {
      return this.undoneTodos.length;
    },
    doneTodoAmount() {
      return this.doneTodos.length;
    }
  }
}
</script>

<style lang="scss">
$colorWhite: #fff;
$colorLightGrey: #ccc;
$colorDark: #35495e;
$colorGreen: #42b883;
$colorRed: #9f2121;

* {
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: $colorDark;
  padding: 1rem;
  margin-top: 30px;
}

h1 {
  font-size: 2.5rem;
  letter-spacing: -.05em;
  padding: 0;
  margin: 0 0 2rem 0;
}

h2 {
  margin-top: 2rem;
}

.todos {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.todo {
  position: relative;
  padding: 1rem 1rem 1rem 4rem;
  margin-bottom: .5rem;
  font-size: 1.2rem;
  color: $colorWhite;
  background: $colorDark;
  border-radius: .2rem;
  transition: background-color 240ms cubic-bezier(.52,.01,.16,1);

  &:hover {
    background-color: darken($colorDark, 10);
  }

  &:active {
    background-color: $colorGreen;
  }

  button {
    cursor: pointer;
    appearance: none;
    font-size: 0;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: transparent;
    background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz48c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IiB2aWV3Qm94PSIwIDAgMTAwIDEwMCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMTAwIDEwMDsiIHhtbDpzcGFjZT0icHJlc2VydmUiPjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+LnN0MHtmaWxsOiNGRkZGRkY7fTwvc3R5bGU+PGc+PHBhdGggY2xhc3M9InN0MCIgZD0iTTUwLDNDMjQuMSwzLDMsMjQuMSwzLDUwczIxLjEsNDcsNDcsNDdzNDctMjEuMiw0Ny00N1M3NS44LDMsNTAsM3ogTTUwLjMsOTEuNkMyNy40LDkxLjYsOC42LDcyLjksOC42LDUwUzI3LjQsOC4zLDUwLjMsOC4zQzczLjIsOC4zLDkyLDI3LDkyLDUwUzczLjIsOTEuNiw1MC4zLDkxLjZ6Ii8+PC9nPjwvc3ZnPg==);
    background-position: center left 1rem;
    background-repeat: no-repeat;
    background-size: 2rem 2rem;
    border: 0 none;
    transition: background-image 240ms cubic-bezier(.52,.01,.16,1);
  }
}

.is-done {
  background-color: $colorGreen;

  &:hover {
    background-color: darken($colorGreen, 10);
  }

  &:active {
    background-color: $colorRed;
  }

  button {
    background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIGZpbGw9IiNGRkZGRkYiIHdpZHRoPSIxMDBwdCIgaGVpZ2h0PSIxMDBwdCIgdmVyc2lvbj0iMS4xIiB2aWV3Qm94PSIwIDAgMTAwIDEwMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4gPGc+ICA8cGF0aCBkPSJtNDQuMTAyIDU4LjY5OWwtOS43MDMxLTkuNjk5Mi0zLjE5OTIgMy4xOTkyIDEyLjkwMiAxMi45MDIgMjcuNS0yNy42MDItMy4yMDMxLTMuMTk5MnoiLz4gIDxwYXRoIGQ9Im01MCAzYy0yNS44OTggMC00NyAyMS4xMDItNDcgNDdzMjEuMTAyIDQ3IDQ3IDQ3IDQ3LTIxLjE5OSA0Ny00Ny0yMS4xOTktNDctNDctNDd6bTAuMzAwNzggODguNjAyYy0yMi45MDIgMC00MS42OTktMTguNzAzLTQxLjY5OS00MS42MDJzMTguNzk3LTQxLjY5OSA0MS42OTktNDEuNjk5YzIyLjg5OCAwIDQxLjY5OSAxOC42OTkgNDEuNjk5IDQxLjY5OXMtMTguODAxIDQxLjYwMi00MS42OTkgNDEuNjAyeiIvPiA8L2c+PC9zdmc+);
  }
}

input[type=text] {
  font-size: 1.25rem;
  width: 100%;
  padding: 1rem;
  border: 1px solid $colorLightGrey;
  border-radius: .2rem;
}

input::placeholder {
  color: $colorLightGrey;
}

form button {
  display: none;
}

.counter {
  font-size: .8rem;
  line-height: 2rem;
  color: $colorWhite;
  display: inline-block;
  width: 2rem;
  height: 2rem;
  text-align: center;
  vertical-align: middle;
  border-radius: 50%;
  background: $colorDark;
}
</style>
