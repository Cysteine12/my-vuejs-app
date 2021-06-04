<template>
    <input :v-model="modelValue" required/>
</template>

<script>
export default {
    name: 'Input',
    props: ['modelValue'],
    emits: ['update:modelValue'],
    data () {
        return {
            user: '',
            country: ''
        }
    }
}
</script>

<style scoped>

input {
    margin: 10px;
    padding: 5px;
    border-radius: 10px;
    border: midnightblue;
    box-sizing: border-box;
    background: #fff;
    width: 100%;
}

</style>