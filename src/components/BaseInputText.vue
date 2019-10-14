<template>
    <input
        type="text"
        class="input"
        :value="value"
        v-on="listeners"
    >
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class BaseInputText extends Vue {
    @Prop() private value!: string;

    get listeners(): object {
        return {
            ...this.$listeners,
            input: (event: any) => this.$emit('input', event.target.value),
        };
    }
}
</script>