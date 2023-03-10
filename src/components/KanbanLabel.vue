<script lang="ts" setup>
import { computed } from "vue"

const props = defineProps<{
    active?: Boolean
    alternative?: Boolean
}>()

const colorschemeDefault = {
    background: "transparent",
    backgroundHover: "var(--kanban-color-bg)",
    logoHover: "var(--color-primary)",
    titleHover: "var(--color-primary)",
    title: "var(--color-grey)",
    logo: "var(--color-grey)",
}

const colorschemeActive = {
    background: "var(--color-primary)",
    backgroundHover: "white",
    logoHover: "var(--color-primary)",
    titleHover: "var(--color-primary)",
    title: "white",
    logo: "white",
}

const colorschemeAlternative = {
    background: "transparent",
    backgroundHover: "transparent",
    logoHover: "var(--text-color)",
    titleHover: "var(--text-color)",
    title: "var(--color-grey)",
    logo: "var(--color-grey)",
}

const getColors = computed(() => {
    if (props.active) return colorschemeActive
    if (props.alternative) return colorschemeAlternative
    return colorschemeDefault
})
</script>

<template>
    <div class="kanban-label">
        <svg
            class="kanban-label__logo"
            width="16"
            height="16"
            xmlns="http://www.w3.org/2000/svg"
        >
            <path
                d="M0 2.889A2.889 2.889 0 0 1 2.889 0H13.11A2.889 2.889 0 0 1 16 2.889V13.11A2.888 2.888 0 0 1 13.111 16H2.89A2.889 2.889 0 0 1 0 13.111V2.89Zm1.333 5.555v4.667c0 .859.697 1.556 1.556 1.556h6.889V8.444H1.333Zm8.445-1.333V1.333h-6.89A1.556 1.556 0 0 0 1.334 2.89V7.11h8.445Zm4.889-1.333H11.11v4.444h3.556V5.778Zm0 5.778H11.11v3.11h2a1.556 1.556 0 0 0 1.556-1.555v-1.555Zm0-7.112V2.89a1.555 1.555 0 0 0-1.556-1.556h-2v3.111h3.556Z"
            ></path>
        </svg>
        <h4 class="kanban-label__title"><slot></slot></h4>
    </div>
</template>

<style lang="scss" scoped>
.kanban-label {
    cursor: pointer;
    display: flex;
    gap: 1rem;
    padding: 1.5rem;
    border-radius: 0 10rem 10rem 0;
    background: v-bind("getColors.background");

    &:hover {
        background: v-bind("getColors.backgroundHover");
    }

    &:hover &__title,
    &:hover &__logo {
        fill: v-bind("getColors.logoHover");
        color: v-bind("getColors.titleHover");
    }

    &__title {
        font-size: 1.5rem;
        color: v-bind("getColors.title");
        font-weight: bold;
    }

    &__logo {
        fill: v-bind("getColors.logo");
    }
}
</style>
