<template>
    <div>
        <v-toolbar></v-toolbar>
        <button @click="getMyBeer" class="buttonBeer">Veux tu ma bière jeune enfant</button>

        <div style="padding-top: 50px">
            <div class="cadreConteneur" v-for="element in beers"
            :key="element.id">
                <span><span class="boldGreen" style="font-weight: bold">Nom de la bière </span>: {{ element.name }} ({{element.abv}}°) :  </span>
                <div class="cadreGrid">
                    <br>
                    <span class="boldRed"> La description voyons : </span>{{ element.description }}
                </div>
                <div class="cadreGrid">
                    <br>
                    <span class="boldBlue">Première fois brassée : </span>{{ element.first_brewed }}
                </div>
                <div class="cadreGrid">
                    <br>
                    <img class="img" v-bind:src="element.image_url">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    /* La classe du composant API.vue */
    export default {
        data(){
            return {
                beers: []
            }
        },
        methods: {
            getMyBeer() {
                axios.get('https://api.punkapi.com/v2/beers')
                    .then((beer) => {
                        console.log(beer.request.response);
                        this.beers = JSON.parse(beer.request.response)
                    })
                    .catch(() => { // function()
                        this.beers = "pas de bière";
                    }
                )
            }
        }
    };
</script>


<style scoped>
    .boldGreen {
        font-weight: bold;
        color: #42b983;
        text-decoration: underline;
        font-size: larger;
    }
    .boldRed{
        font-weight: bold;
        color: crimson;
        text-decoration: underline;
        font-size: larger;
    }
    .boldBlue{
        font-weight: bold;
        color: blue;
        text-decoration: underline;
        font-size: larger;
    }
    .cadreConteneur{
        display: grid;
        grid-template-columns: auto auto auto;
        padding: 10px;
    }
    .cadreGrid {
        border: 1px solid rgba(0, 0, 0, 0.8);
        padding: 20px;

        text-align: center;
    }
    .img{
        width: auto;
        height: 300px;
    }
    .buttonBeer{
        font-size: 24px;
        font-family: "Bauhaus 93";
        color: white;
        background: linear-gradient(#FFC465, #FFBB4D);
        background-image: linear-gradient(to right, #4CB8C4 0%, #3CD3AD 51%, #4CB8C4 100%);
        transition-duration: 0.4s;
        width: 550px;
        height: 75px;

    }
    .buttonBeer:hover{
        background-position: right center;
        background-color: black;
        border-radius: 50px;
        box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24), 0 17px 50px 0 rgba(0,0,0,0.19);
    }

</style>