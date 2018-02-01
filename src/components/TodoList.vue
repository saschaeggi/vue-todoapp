<template>
    <ul class="todos">
        <li
            class="todo"
            v-for="todo in todos.reverse()"
            v-bind:key="todo.id"
            v-bind:class="{ 'is-done ' : todo.done }"
        >
        {{ todo.title }}
        
        <button
            v-on:click="toggleDone(todo)">
            <span v-if="!todo.done">Done!</span>
            <span v-if="todo.done">Undone!</span>
        </button>
      </li>
    </ul>
</template>

<script>
export default {
    props: [
        'todos'
    ],
    methods: {
        toggleDone(todo) {
             this.$emit('toggleDone', todo)
        }
    }
}
</script>

<style>

</style>
