<script setup>

</script>


<template>
    <button>
        <a href="./">
            <slot></slot>
        </a>
    </button>
</template>


<style lang='scss' scoped>
button{
    background-color: var(--color-dark);
    color: var(--color-gray);
    border: none;
    
    cursor: pointer;
    a{
        color: var(--color-gray) !important;
        font-family: 'Lexend Deca', sans-serif;
        font-weight: light;
        text-decoration: none;
        display: block;
        padding: 10px 25px;
    }
}

</style>