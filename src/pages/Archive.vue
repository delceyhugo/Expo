<script setup>

import { ref } from 'vue';

const gallery = ref(null);

const fields = [
    'id',
    'title',
    'image_id',
    'artist_display',
    'artist_title',
    'artwork_type_title',
]
// https://www.artic.edu/iiif/2/{identifier}/full/843,/0/default.jpg

fetch(`https://api.artic.edu/api/v1/artworks/search?q=french&fields=${fields.join(',')}&limit=4`)
    .then(response => response.json())
    .then(data => gallery.value = data);

</script>


<template>
    <div id="archive" v-if="gallery">
        <section id="first">
            <header>
                <h2>Europeana</h2>
                <h1>Birmingham museum</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[0].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[0].title>
            </main>
            <footer>
                <a href="">
                    <span>Read more</span>
                    <span>⭢</span>
                </a>
            </footer>
        </section>

        <section id="second">
            <header>
                <h2>Europeana</h2>
                <h1>A Woman Slicing Bread</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[1].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[1].title>
            </main>
            <aside>
                <p>
                    Date: 1800. institution: Rijks Museum, Provider: Rijks Museum, providing country: Netherlands, public domain
                </p>
            </aside>
            <footer>
                <a href="">
                    <span>Read more</span>
                    <span>⭢</span>
                </a>
            </footer>
        </section>

        <section id="third">
            <header>
                <h2>Europeana</h2>
                <h1>A Woman Slicing Bread</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[2].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[2].title>
            </main>
            <aside>
                <p>
                    Date: 1800. institution: Rijks Museum, Provider: Rijks Museum, providing country: Netherlands, public domain
                </p>
            </aside>
            <footer>
                <a href="">
                    <span>Read more</span>
                    <span>⭢</span>
                </a>
            </footer>
        </section>

        <section id="fourth">
            <header>
                <h2>Europeana</h2>
                <h1>A Woman Slicing Bread</h1>
            </header>
            <main>
                <img :src="`https://www.artic.edu/iiif/2/${gallery.data[3].image_id}/full/500,/0/default.jpg`" :alt=gallery.data[3].title>
            </main>
            <aside>
                <p>
                    Date: 1800. institution: Rijks Museum, Provider: Rijks Museum, providing country: Netherlands, public domain
                </p>
            </aside>
            <footer>
                <a href="">
                    <span>Read more</span>
                    <span>⭢</span>
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
        "first second second"
        "first third fourth";
    grid-template-rows: 1fr 1fr;
    grid-template-columns: 1fr 1fr 1fr;
    padding: 8px;

    section{
        margin: 8px;
        padding: 30px;
        border-radius: 30px;
        color: #342415;
        header{
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            h2{
                font-family: "Lexend Deca", sans-serif;
                font-style: normal;
                font-size: 1em;
                font-weight: 300;
                text-transform: uppercase;
                border: 1px solid var(--color-dark);
                border-radius: 25px;
                padding: 0px 5px;
            }
            
        }
        main{
            border-radius: 30px;
            overflow: hidden;
            background-color: brown;
            img{
                object-fit: cover;
            }
        }
        footer{
            a{
                display: flex;
                align-items: center;
                justify-content: space-between;
            }
        }
    }

    #first{
        background: #e0d6c2;
        grid-area: first;
        display: flex;
        flex-direction: column;
    }
    #second{
        background: #8f8868;
        grid-area: second;

        display: grid;
        grid-template-areas: 
            "header main"
            "aside main"
            "footer footer";
        header{

        }
        main{
            
        }
        aside{

        }
        footer{

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
}

</style>