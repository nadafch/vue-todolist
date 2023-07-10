<script setup>

</script>
<template>
    <button>
        <slot>Create</slot>
    </button>
</template>



<style lang="scss" scoped>
button {
    padding: 3px 10px;
    font-weight: 600;
    border: none;
    border-radius: 100px;
    margin-left: 5px;

    &:hover {
        background-color: #41b0809c;
    }
}
</style>