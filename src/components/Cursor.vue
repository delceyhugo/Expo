<script setup>
import { onMounted } from 'vue'

onMounted(() => {
    const cursor = document.querySelector('#mouse')
    let currentStyle = "default"
    document.addEventListener('mousemove', (e) => {
        if(currentStyle == "default") cursor.style.transform = `translate(${e.clientX - cursor.offsetWidth / 2}px, ${e.clientY - cursor.offsetHeight / 2}px)`
        if(currentStyle == "link"){
            cursor.style.transform = `translate(${e.clientX - cursor.offsetWidth / 2}px, ${e.clientY - cursor.offsetHeight / 2}px) scale(3)`
        }
    })
    window.addEventListener('mousedown', () => {
        cursor.classList.add('cursor--click')
    })
    window.addEventListener('mouseup', () => {
        cursor.classList.remove('cursor--click')
    })
    window.addEventListener('mouseover', (e) => {
        if(e.target.tagName === 'A') currentStyle = "link", cursor.classList.add('cursor--link')
        if(e.target.classList.contains('cursor-link')) currentStyle = "link", cursor.classList.add('cursor--link')
    })
    window.addEventListener('mouseout', (e) => {
        currentStyle = "default", cursor.classList.remove('cursor--link')
    })
})

</script>


<template>
    <div id="mouse">
    </div>
</template>


<style lang='scss' scoped>
#mouse{
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: var(--color-gray);
    transform-origin: center;
    position: fixed;
    z-index: 9999;
    pointer-events: none;

    transition: all 100ms ease;
    transform: translate(-50%, -50%) scale(.3);
    mix-blend-mode: difference;
    touch-action: none;

    &.cursor--link {
        border: 1px solid var(--color-gray);
    }
    &.cursor--click {
        background-color: var(--color-dark);
        border: 1px solid var(--color-gray);
    }
}

</style>