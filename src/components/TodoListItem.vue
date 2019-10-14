<template>
    <li>
        {{ todo.text }}
        <button v-on:click="$emit('remove',todo.id)">
            X
        </button>
    </li>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class TodoListItem extends Vue {
     @Prop() private todo!: object;
}
</script>