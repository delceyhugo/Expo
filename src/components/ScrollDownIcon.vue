<script setup>

</script>

<template>
    <div id="scroll-down-icon">
        <div class="paralax-container" data-paralax="90">
            <div class="scroll-down-icon">
            </div>
        </div>
    </div>
</template>

<style lang='scss' scoped>
#scroll-down-icon{
    position: absolute;
    bottom: 10px;
    width: 100vw;
    display: flex;
    justify-content: center;
    // z-index: 3;
    .scroll-down-icon{
        width: 50px;
        height: 90px;
        border: 3px solid #333;
        border-radius: 60px;
        position: relative;
        transform: scale(0.7);

        background: linear-gradient(to bottom, rgba(255, 255, 255, 0) 50%, var(--color-dark) 50%) top;
        background-size: 100% 300%;
        background-position: 50% 0%;
        transition: .3s ease-out;
        &:hover{
            background-position: 50% 100%;
            color: var(--color-gray);
        }
        &::before {
            content: '';
            width: 12px;
            height: 12px;
            position: absolute;
            top: 10px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #333;
            border-radius: 50%;
            opacity: 1;
            animation: wheel 2s infinite;
            -webkit-animation: wheel 2s infinite;
            @-webkit-keyframes wheel {
                to {
                    opacity: 0;
                    top: 60px;
                }
            }
            @keyframes wheel {
                to {
                    opacity: 0;
                    top: 60px;
                }
            }
        }
    }
}
</style>