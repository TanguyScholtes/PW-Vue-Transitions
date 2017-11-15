<template>
    <div>
        <ul>
            <li v-for="character in characters.results">
                {{ character.name }}
            </li>
        </ul>
        <p>
            <span v-if="characters.previous" @click="loadCharacters( characters.previous )">Previous</span>
            <span v-if="characters.previous && characters.next"> | </span>
            <span v-if="characters.next" @click="loadCharacters( characters.next )">Next</span>
        </p>
    </div>
</template>

<script>
    export default {
        name: 'AnimationList',

        props: {
            characters: {
                type: Object,
                required: true
            }
        },

        methods: {
            loadCharacters ( string ) {
                this.$emit( 'loadCharacters', string );
            }
        }
    }
</script>

<style lang="scss">

</style>
