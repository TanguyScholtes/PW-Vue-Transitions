<template>
    <div id="app">
        <h1 class="site-title">Star Wars Api</h1>

        <div class="info">
            <p>This exercice uses the API at <a href="https://swapi.co/">SWAPI.co</a></p>
            <p><a href="https://vuejs.org/v2/guide/transitions.html">Read Vue Transitions Guide</a></p>
        </div>

        <form class="interface" method="" action="" @submit.prevent>
            <select v-model="animation">
                <option value="fade">Fade</option><!-- transition -->
                <option value="slide">Slide</option><!-- animation -->
            </select>

            <button @click="loadCharacters( url )">Load Star Wars Characters</button>
        </form>

        <transition :name="animation" mode="out-in">
            <component
                :is="currentComponent"
                :key="currentComponent"
                v-bind="currentProps"
                @loadCharacters="loadCharacters"
                class="characters-list"
            ></component>
        </transition>


    </div>
</template>

<script>
    import AnimationLoading from './AnimationLoading.vue';
    import AnimationList from './AnimationList.vue';
    import Axios from 'axios';

    export default {
        name: 'App',

        components: {
            AnimationLoading,
            AnimationList
        },

        data () {
            return {
                animation: 'fade',
                currentComponent: '',
                characters: {},
                url: 'https://swapi.co/api/people/'
            }
        },

        computed: {
            currentProps () {
                if ( this.currentComponent === 'animation-loading' ) {
                    return {};
                } else {
                    return {
                        characters: this.characters
                    };
                }
            }
        },

        methods: {
            loadCharacters ( url ) {
                this.currentComponent = 'animation-loading';
                Axios.get( url )
                    .then( response => {
                        this.characters = response.data;
                        this.currentComponent = 'animation-list';
                    } )
                    .catch( function ( error ) {
                        console.log( error );
                    } );
            }
        }
    }
</script>

<style lang="scss">
    @font-face {
        font-family: 'Starjedi';
        src: url('/src/assets/fonts/starjedi/starjedi.ttf')  format('truetype'); /* Safari, Android, iOS */
    }
    @font-face {
        font-family: 'Open Sans';
        src: url('/src/assets/fonts/opensans/OpenSans-Regulat.ttf')  format('truetype'); /* Safari, Android, iOS */
    }
    #app{
        font-family: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
    }
    .info, .site-title{
        text-align: center;
    }
    .site-title{
        font-family: "Starjedi", "Helvetica Neue", Helvetica, Arial, sans-serif;
        font-size: 3em;
    }
    .characters-list, .interface{
        width: 80%;
        max-width: 1350px;
        margin: 0 auto;
    }
    .characters-list{
        background-color: #a2cee0;
        border-radius: 1em;
        border: darken( #a2cee0, 15% );
        padding: 1em;
        min-height: 17em;
    }
    .interface{
        & *{
            display: block;
            margin: 1em 0;
        }
        & select{
            width: 100%;
            padding: 0.5em;
        }
        & button{
            color: white;
            padding: 1em;
            background-color: rgb(32, 74, 226);
            border-radius: 0.5em;
            border: none;
            &:hover{
                background-color: rgb(19, 50, 162);
            }
        }
    }

    .fade-enter-active, .fade-leave-active{
        transition: opacity .2s;
    }
    .fade-enter-to{
        opacity: 1; //facultatif car 1 par défaut
    }
    .fade-enter, .fade-leave-to{
        opacity: 0;
    }

    .slide-enter-active{
        animation: slide .2s ease;
        //transition: all .3s ease;
    }
    .slide-leave-active{
        animation: slide .2s ease reverse;
        //transition: all .8s ease;
    }
    .slide-enter, .slide-leave-to{
        //transform: translateX(120%);
    }

    @keyframes slide {
        0% {
            transform: translateX( 80% );
        }
        100% {
            transform: translateX( 0 );
        }
    }
</style>
