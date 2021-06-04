<template>
    <div class="backdrop">
        <div class="alert">
            <slot></slot>
        </div>
    </div>
</template>

<style scoped>

.backdrop {
    margin: auto;
    display: flex;
    flex-direction: column;
}
.alert {
    margin: auto;
    padding: 30px;
    border: 3px inset rgb(56, 2, 44);
    border-radius: 10px;
    background: mediumslateblue;
    color: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    align-self: center;
    justify-content: center;
    position: absolute;
    top: 200px;

    z-index: 2;
}

</style>