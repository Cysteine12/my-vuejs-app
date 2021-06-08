<template>
    <button :style="{ background: bgcolor, color: color }">
        {{ content }}
        <slot></slot>
    </button>
</template>

<script>
export default {
    props: ['content', 'bgcolor', 'color']
}
</script>

<style scoped>
button {
    margin: 5px;
    border: 1.5px solid #2c3e50;
    border-radius: 5px;
    padding: 3px;
    cursor: pointer;
}
</style>
