<script setup>

import { ref, onMounted } from 'vue';

const gallery = ref(null);
const tabs = ref(2);

const fields = [
    'id',
    'title',
    'image_id',
    'artist_display',
    'artist_title',
    'artwork_type_title',
    'place_of_origin',
    'provenance_text'
]
// https://www.artic.edu/iiif/2/{identifier}/full/843,/0/default.jpg
// <img :src="`https://www.artic.edu/iiif/2/${gallery.data[0].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[0].title>



const fetchData = (request) => {
    fetch(`https://api.artic.edu/api/v1/artworks/search?q=${request}&fields=${fields.join(',')}&limit=4`)
    .then(response => response.json())
    .then(data => {
        gallery.value = data
    });
}
const truncateString = (string, length) => {
  if (string?.length > length) {
    return `${string.slice(0, length)}...`;
  } else return string;
}

fetchData('roman')



</script>


<template>
    <div id="archive" v-if="gallery">
        <header>
            <ul>
                <h1>Art Archive</h1>
                <li @click="tabs = 1, fetchData('ancientgreece')" :class="`cursor-link ${tabs == 1 ? 'active-section': null}`">Ancient Greece</li>
                <li @click="tabs = 2, fetchData('roman')" :class="`cursor-link ${tabs == 2 ? 'active-section': null}`">Roman</li>
                <li @click="tabs = 3, fetchData('vangogh')" :class="`cursor-link ${tabs == 3 ? 'active-section': null}`">Van Gogh</li>
            </ul>
            <li @click="$emit('changePage', 'hero')" class="cursor-link" href="">Home</li>
        </header>


        <section id="first">
            <header>
                <h2>{{ gallery.data[0].place_of_origin }}</h2>
                <h1>{{ gallery.data[0].title }}</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[0].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[0].title>
            </main>
            <footer>
                <a href="">
                    <span class="cursor-link">Read more</span>
                    <span class="cursor-link">⭢</span>
                </a>
            </footer>
        </section>

        <section id="second">
            <header>
                <h2>{{ gallery.data[1].place_of_origin }}</h2>
                <h1>{{ gallery.data[1].title }}</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[1].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[1].title>
            </main>
            <aside>
                <p>
                    {{ truncateString(gallery.data[1].provenance_text, 180) }}
                </p>
            </aside>
            <footer>
                <a href="">
                    <span class="cursor-link">Read more</span>
                    <span class="cursor-link">⭢</span>
                </a>
            </footer>
        </section>

        <section id="third">
            <header>
                <h2>{{ gallery.data[2].place_of_origin }}</h2>
                <h1>{{ truncateString(gallery.data[2].title, 25) }}</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[2].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[2].title>
            </main>
            <aside>
                <p>
                    {{ truncateString(gallery.data[2].provenance_text, 100) }}
                </p>
            </aside>
            <footer>
                <a href="">
                    <span class="cursor-link">Read more</span>
                    <span class="cursor-link">⭢</span>
                </a>
            </footer>
        </section>

        <section id="fourth">
            <header>
                <h2>{{ gallery.data[3].place_of_origin }}</h2>
                <h1>{{ truncateString(gallery.data[3].title, 25) }}</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[3].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[3].title>
            </main>
            <aside>
                <p>
                    {{ truncateString(gallery.data[3].provenance_text, 100) }}
                </p>
            </aside>
            <footer>
                <a href="">
                    <span class="cursor-link">Read more</span>
                    <span class="cursor-link">⭢</span>
                </a>
            </footer>
        </section>

    </div>
</template>


<style lang='scss' scoped>

#archive{
    background: var(--color-dark);
    height: 100vh;
    overflow: hidden;
    display: grid;
    z-index: 2;
    grid-template-areas: 
        "header header header"
        "first second second"
        "first third fourth";
    grid-template-rows: auto 1fr 1fr;
    grid-template-columns: 1fr 1fr 1fr;
    padding: 8px;


    >header{
        grid-area: header;
        display: flex;
        flex-direction: row;
        align-items: flex-start;
        justify-content: space-between;
        border: 2px solid #baa690;
        border-radius: 30px;
        color: #baa690;
        ul{
            display: flex;
            flex-direction: row;
            gap: 2px;
            align-items: center;
            h1{
                font-family: "Lexend Deca", sans-serif;
                font-style: normal;
                font-size: 28px;
                font-weight: 300;
                text-transform: uppercase;
                background-color: #333124;
                border-radius: 30px;
                padding: 4px 3vw;
            }
        }
        li{
            list-style: none;
            border: 2px solid #baa690;
            border-radius: 30px;
            padding: 8px 3vw;
            margin: 2px 2px;
            cursor: pointer;
            color: #baa690;
            font-family: "Lexend Deca", sans-serif;
            font-style: normal;
            font-size: 18px;
            font-weight: 300;
            transition: all 200ms ease;
            background: linear-gradient(to top, rgba(255, 255, 255, 0) 50%, #baa690 50%) bottom;
            background-size: 100% 300%;
            background-position: 50% 90%;
            transition: .3s ease-out;
            &:hover{
            background-position: top;
            color: var(--color-dark);
            }
            &.active-section{
                background-color: #baa690;
                color: var(--color-dark);
            }
        }
    }
    
    section{
        margin: 8px;
        padding: 30px;
        border-radius: 30px;
        color: #342415;
        gap: 20px;
        position: relative;


        header{
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            gap: 20px;
            h2{
                font-family: "Lexend Deca", sans-serif;
                font-style: normal;
                font-size: 18px;
                font-weight: 300;
                text-transform: uppercase;
                border: 1px solid var(--color-dark);
                border-radius: 25px;
                padding: 0px 10px;
            }
            h1{
                font-size: 29px;
                font-weight: 800;
            }
            
        }
        main{
            position: relative;
            border-radius: 30px;
            display: flex;
            justify-content: center;
            overflow: hidden;
            width: 100%;
            box-shadow: 4px 4px 10px 2px rgba(87, 82, 82, 0.5);
            img{
                position: absolute;
                height: 100%;
                width: 100%;
                display: block;
                object-fit: cover;
            }
        }
        aside{
            p{
                font-size: 20px;
                text-overflow: ellipsis;
            }
        }
        footer{
            a{
                display: flex;
                align-items: center;
                justify-content: space-between;
                margin-top: 20px;
            }
            &::before{
                content: "";
                opacity: 0.3;
                left: 0;
                position: absolute;
                display: block;
                width: 100%;
                height: 2px;
                background-color: #342415;
            }
        }
    }

    #first{
        background: #e0d6c2;
        grid-area: first;
        display: flex;
        flex-direction: column;
        main{flex: 1;}
    }
    #second{
        background: #8f8868;
        grid-area: second;

        display: grid;
        grid-template-areas: 
            "header main"
            "aside main"
            "footer footer";
        grid-template-rows: 1fr 1fr;
        grid-template-columns: 1fr 1fr;
        header{
            grid-area: header;
        }
        main{
            grid-area: main;
        }
        aside{
            grid-area: aside;
        }
        footer{
            grid-area: footer;
        }
    }
    #third{
        background: #976c54;
        grid-area: third;

    }
    #fourth{
        background: #b5a38c;
        grid-area: fourth;
    }
    #third, #fourth{
        display: grid;
        grid-template-areas: 
            "header main"
            "aside main"
            "footer footer";
        grid-template-rows: auto 1fr auto;
        grid-template-columns: 1fr 1fr;
        header{
            grid-area: header;
        }
        main{
            grid-area: main;
        }
        aside{
            grid-area: aside;
        }
        footer{
            grid-area: footer;
        }
    }
}

</style>