<template>
    <div id="pokemon">
        <!--
        <h1> {{num}} {{name | upper}} </h1>
        <small> {{url}} </small>
        -->

        <div class="card">
        <div class="card-image">
            <!--
            <figure>
                <figure class="image is-4by3">
                <img src="https://bulma.io/images/placeholders/1280x960.png" alt="Placeholder image">
            </figure>
            -->
            <figure>
                <!--
                <img :src="pokemon.front" alt="Placeholder image">            
                <img :src="pokemon.back" alt="Placeholder image">            
                -->
                <img :src="currentImg" alt="Placeholder image">            
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{num}} - {{name | upper}}</p>
                <p class="subtitle is-6">Type: {{pokemon.type | upper}}</p>
                <!--
                    <p class="subtitle is-6">{{this.pokemon.type}}</p>
                -->
            </div>
            </div>

            <div class="content">
                <div class="buttons is-centered">
                    <button class="button is-link is-rounded " @click="mudarSprite">Turn Pokemon</button>
                </div>
            </div>
        </div>
        </div>

    </div>
</template>

<script>
import axios from 'axios';

export default {
    created: function() {
        axios.get(this.url).then(res => {
            //console.log(res);
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;

            //console.log(this.pokemon);
        })
    },
    data() {
        return{
            isfront: true,
            currentImg: "",
            pokemon: {
                type: "",
                front: "",
                back: ""
            }
        }
    }, 
    props: {
        num: Number,
        name : String,
        url: String
    },
    filters: {
        upper: function(value) {
            var newName = value.substring(0,1).toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods: {
        mudarSprite: function() {
            if(this.isfront) {
                this.isfront = false;
                this.currentImg = this.pokemon.back;
            } else {
                this.isfront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
    #pokemon {
        margin-top: 2%;
    }
</style>