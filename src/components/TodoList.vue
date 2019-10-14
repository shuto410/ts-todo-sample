<template>
    <div>
        <BaseInputText
            v-model="newTodoText"
            placeholder="New todo"
            @keydown.enter="addTodo"
        />
        <ul v-if="this.todos.length">
            <TodoListItem
                v-for="todo in this.todos"
                :key="todo.id"
                :todo="todo"
                @remove="removeTodo"
            />
        </ul>
        <p v-else>
           Nothing left in the list,
        </p>
    </div>
</template>

<script lang="ts">
import BaseInputText from '@/components/BaseInputText.vue';
import TodoListItem from '@/components/TodoListItem.vue';
import { Component, Prop, Vue } from 'vue-property-decorator';


let nextTodoId = 1;
@Component({
    components: {
        BaseInputText,
        TodoListItem,
    },
})

export default class TodoList extends Vue {
    private newTodoText: string = '';
    private todos: Array<{ id: number , text: string}> = [
        {
            id: nextTodoId++,
            text: 'Learn Vue',
        },
        {
            id: nextTodoId++,
            text: 'Learn about single-file components',
        },
        {
            id: nextTodoId++,
            text: 'Fall in love',
        },
    ];

    private addTodo(): void {
        const trimmedText = this.newTodoText.trim();
        if (trimmedText) {
            this.todos.push({
                id: nextTodoId++,
                text: trimmedText,
            });
            this.newTodoText = '';
        }
    }

    private removeTodo(idToRemove: number): void {
        this.todos = this.todos.filter((todo) => {
            return todo.id !== idToRemove;
        });
    }
}
</script>