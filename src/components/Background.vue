<script setup>
import { onMounted, defineExpose } from 'vue'
let canvas
let ctx
let divider
let delay = 70
let section = 0

onMounted(() => {
    canvas = document.getElementById('transition-canvas')
    ctx = canvas.getContext('2d')
    init()
    
    DrawGrid(false, "rgb(25 25 25)", 0.05)
    // setTimeout(() => DrawGrid(true, "rgb(25 25 25)", 1), 3000);
    // setTimeout(() => ClearGrid(), 5000);

    let sumDelta = 0
    setTimeout(() => {
        window.addEventListener('wheel', (e) => {

            // const scrollDownIcon = document.querySelector('.scroll-down-icon');
            // if(e.wheelDelta < 0){
            //     if(sumDelta < 100) sumDelta = sumDelta + (-e.wheelDelta / 8)
            //     if(sumDelta > 100) sumDelta = 100
            //     console.log(sumDelta);
                
            //     scrollDownIcon.style.backgroundPosition = `50% ${sumDelta}%`
            // }


            // Vers le bas
            // if(e.wheelDelta < 0){
            //     if(section == 0){
            //         console.log("Vers le bas")
            //         section = 1
            //         DrawGrid(true, "rgb(25 25 25)", 1)
            //     }
                // if(section == 1){
                //     ClearGrid()
                //     section++
                // }
    
    
        })
    }, 3000);

    window.addEventListener('resize', () => {
        init()
        DrawGrid(false, "rgb(25 25 25)", 0.05)
    })
})

const init = () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    canvas.width = canvas.parentNode.offsetWidth
    canvas.height = canvas.parentNode.offsetHeight

    divider = Math.floor(window.innerWidth / 100);
    if (divider % 2 === 0) {
        divider++;
    }
    ctx.translate((canvas.width/2) - ((canvas.width/divider)/2), window.innerHeight);
}

/**
 * Draws a grid on the canvas and optionally fills it.
 * Sets the alpha transparency of the context depending on the fill parameter.
 * Iteratively draws and optionally fills rectangles and lines on the canvas.
 * @param {CanvasRenderingContext2D} ctx - The canvas context.
 * @param {boolean} fill - Whether to fill the grid rectangles or not.
 * @returns {undefined}
 */
const DrawGrid = (fill, color, alpha) => {
    ctx.globalAlpha = alpha
    fill ? ctx.fillStyle = color : ctx.strokeStyle = color
    fill ? canvas.style.zIndex = '99' : canvas.style.zIndex = '0'

    // Top
    let j = 0
    let jInterval = setInterval(() => {
        fill ? ctx.fillRect(0, j * (-window.innerWidth / divider), window.innerWidth / divider, -window.innerWidth / divider) : null

        ctx.strokeRect(0, j * (-window.innerWidth / divider), window.innerWidth / divider, -window.innerWidth / divider);
        DrawLines(j * (-window.innerWidth / divider), fill);
        j++
        if (j > divider) {clearInterval(jInterval)}
    }, delay)
}
/**
 * Draws lines on the sides of the grid and optionally fills them.
 * @param {CanvasRenderingContext2D} ctx - The canvas context.
 * @param {number} j - The y-coordinate of the line to be drawn.
 * @param {boolean} fill - Whether to fill the rectangles or not.
 * @returns {undefined}
 */
const DrawLines = (j, fill) => {
    // Sides
    let i = 1
    let iInterval = setInterval(() => {

        ctx.strokeRect(i * window.innerWidth / divider, j, window.innerWidth / divider, -window.innerWidth / divider);
        ctx.strokeRect(-(i * window.innerWidth / divider), j, window.innerWidth / divider, -window.innerWidth / divider);
        fill ? ctx.fillRect(i * window.innerWidth / divider, j, window.innerWidth / divider, -window.innerWidth / divider) : null
        fill ? ctx.fillRect(-(i * window.innerWidth / divider), j, window.innerWidth / divider, -window.innerWidth / divider) : null
   
        i++
        if (i > divider) {clearInterval(iInterval)}
    }, delay)
}

/**
 * Clears the entire grid by drawing white squares over it
 * @param {CanvasRenderingContext2D} ctx - the canvas context
 * @returns {undefined}
 */
const ClearGrid = () => {
    let j = 0
    let jInterval = setInterval(() => {
        ctx.clearRect(0, j * (-window.innerWidth / divider), window.innerWidth / divider, -window.innerWidth / divider)
        ClearLines(j * (-window.innerWidth / divider));
        j++
        if (j > divider) {clearInterval(jInterval)}
    }, delay)
}
/**
 * Clears a line of the grid by drawing white squares over it
 * @param {CanvasRenderingContext2D} ctx - the canvas context
 * @param {number} j - the y-coordinate of the line to be cleared
 * @returns {undefined}
 */
const ClearLines = (j) => {
    let i = 1
    let iInterval = setInterval(() => {
        ctx.clearRect(i * window.innerWidth / divider, j, window.innerWidth / divider, -window.innerWidth / divider)
        ctx.clearRect(-(i * window.innerWidth / divider), j, window.innerWidth / divider, -window.innerWidth / divider)
        i++
        if (i > divider) {clearInterval(iInterval)}
    }, delay)
}



defineExpose({
    DrawGrid,
    ClearGrid
})




</script>


<template>
    <canvas id="transition-canvas">
    </canvas>
</template>


<style lang='scss' scoped>
canvas{
    position: absolute;
    z-index: 0;
}
</style>