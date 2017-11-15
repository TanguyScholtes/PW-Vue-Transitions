<template>
    <div id="app">
        <h1 class="site-title">Star Wars Api</h1>

        <footer class="footer">
            <p>This exercice uses the API at <a href="https://swapi.co/">SWAPI.co</a></p>
            <p><a href="https://vuejs.org/v2/guide/transitions.html">Read Vue Transitions Guide</a></p>
        </footer>
    </div>
</template>

<script>
    export default {
        name: 'app',
    }
</script>

<style lang="scss">
    @font-face {
        font-family: 'Starjedi';
        src: url('/src/assets/fonts/starjedi/starjedi.ttf')  format('truetype'); /* Safari, Android, iOS */
    }
    .footer, .site-title{
        text-align: center;
    }
    .site-title{
        font-family: "Starjedi", "Helvetica Neue", Helvetica, Arial, sans-serif;
        font-size: 3em;
    }
</style>
