<script setup>
import Logo from '../components/Logo.vue'
import Button from '../components/Button.vue'
import TransitionBox from '../components/Background.vue'
import { onMounted, ref, defineEmits } from 'vue';
import ScrollDownIcon from '../components/ScrollDownIcon.vue';

const transitionBoxRef = ref(false)

onMounted(() => {
  let paralax = document.querySelectorAll('.paralax-container')
  window.addEventListener('mousemove', (e) => {
    paralax.forEach((el) => {
      const position = el.getAttribute('data-paralax')
      el.style.transform = `translateX(${((window.innerWidth/2) - e.pageX) / position}px) translateY(${((window.innerHeight/2) - e.pageY) / position}px)`
    })
  })
  setTimeout(() => {
    document.querySelector('.counter').style.setProperty('--num', 120)
  }, 100)
})

defineEmits(['changePage'])

</script>


<template>
  <div id="hero">
    <TransitionBox ref="transitionBoxRef" />
    <header>
      <aside class="paralax-container" data-paralax="90">
        <Logo />
        <span></span>
        <a href="./">Menu</a>
      </aside>
      <nav class="paralax-container" data-paralax="90">
        <a href="./">Sale</a>
        <Button>Contact</Button>
      </nav>
    </header>
    <main>
      <div class="paralax-container" data-paralax="30">
        <h1>LIGHT<span>&</span>LIFE</h1>
        <h1 class="secondary">CAPTURED</h1>
        <h1>BY LENS</h1>
      </div>
      <footer>
        <h2 id="quote" class="paralax-container" data-paralax="95">
          The <i>largest</i> digital art gallery in the <i>world</i>
        </h2>
        <div id="exhibitions" class="paralax-container" data-paralax="95">
          <h2><span class="counter"></span> <br> Exibitions</h2>
          <span></span>
          <aside class="cursor-link">
            <h3 class="cursor-link">✤</h3>
            <p class="cursor-link">New expo on monday at 21.03 - 10.00</p>
            <svg width="24" height="24" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="cursor-link feather feather-arrow-up-right">
              <line x1="7" y1="17" x2="17" y2="7"></line>
              <polyline points="7 7 17 7 17 17"></polyline>
            </svg>
          </aside>
        </div>
        <div @click="$emit('changePage', 'archive')" id="art-archive" class="paralax-container cursor-link" data-paralax="95">
          <img class="cursor-link paralax-container" src="../assets/camera.png" alt="Camera" data-paralax="85">
          <p class="cursor-link">Art archive</p>
        </div>
      </footer>
    </main>
    <ScrollDownIcon />
  </div>
</template>


<style lang='scss' scoped>
@property --num {
  syntax: "<integer>";
  initial-value: 0;
  inherits: false;
}

#hero{
  

  background: linear-gradient(145deg, #b5c3df 0%, #dbe3e1 100%);


  height: 100%;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  z-index: 2;
  >header{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 100%;
    padding: 30px 5vw;
    z-index: 2;
    aside{
      display: flex;
      flex-direction: row;
      align-items: center;
      gap: 40px;
      a{
        padding: 10px 15px;
      }
      >span{
        width: 1px;
        height: 40px;
        opacity: 0.5;
        background-color: #191919;
      }
      
    }
    nav{
      display: flex;
      flex-direction: row;
      align-items: center;
      gap: 30px;
      a{
        padding: 10px 15px;
      }
    }
  }
  >main{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    flex: 1;
    z-index: 1;
    div{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      flex: 1;
      >h1{
        font-family: "Noto Serif Display", serif;
        font-weight: 400;
        font-size: 175px;
        line-height: 0.8em;
        text-transform: uppercase;
        color: var(--color-dark);
        >span{
          font-weight: 300;
          font-size: 110px;
        }
        &.secondary{
          font-family: "Lexend Deca", sans-serif;
          font-weight: 300;
          font-style: italic;
        }
      }
    }
    footer{
      position: relative;
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
      gap: 100px;
      #quote{
        font-family: "Lexend Deca", sans-serif;
        font-weight: 200;
        font-size: 25px;
        max-width: 200px;
        flex: 1;
      }
      #exhibitions{
        background-color: #e6e8eb;
        flex: 1;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 35px;
        padding: 50px 5vw;
        h2{
          font-weight: 300;
          text-transform: uppercase;
          font-size: 50px;
          text-align: center;
          .counter{
            transition: --num 4s ease-out;
            counter-set: num var(--num);
            &::after {
              content: counter(num);
            }
          }
        }
        >span{
          width: 100%;
          height: 2px;
          opacity: 0.5;
          background-color: #191919;
          opacity: 0.2;
        }
        aside{
          display: flex;
          flex-direction: row;
          align-items: center;
          gap: 10px;
          cursor: pointer;
          h3{
            font-weight: 600;
            font-size: 35px;
            color: var(--color-dark);
          }
          p{
            max-width: 200px;
          }
          svg{
            stroke: var(--color-dark);
          }
          background: linear-gradient(to top, rgba(255, 255, 255, 0) 50%, var(--color-dark) 50%) bottom;
          background-size: 100% 300%;
          background-position: 50% 90%;
          transition: .3s ease-out;
          &:hover{
            background-position: top;
            color: var(--color-gray);
            svg{
              stroke: var(--color-gray);
            }
            h3{
              color: var(--color-gray);}
          }
        }
      }
      #art-archive{
        display: flex;
        position: relative;
        flex: 1;
        flex-direction: row;
        justify-content: center;
        align-items: center;

        cursor: pointer;
        &:hover{
          p{
            text-decoration: underline;
            &::after {
              background-color: var(--color-dark);
            }
          }
          img{
            transform: translate(-15%, -15%) scale(1.1);
          }
        }
        img{
          width: 100px;
          height: auto;
          object-fit: cover;
          z-index: 2;
          transform: translate(-15%, -15%);
          transition: all 0.3s ease-out;
        }
        p{
          &::after {
            transition: all 0.3s ease-out;
            content: '';
            position: absolute;
            top: 10px;
            left: 10px;
            width: 75px;
            height: 75px;
            background-color: #e6e8eb;
            z-index: 1;
            border-radius: 2px;
          }
        }
      }
    }
  }
}
</style>