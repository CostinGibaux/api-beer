<template>
    <v-app dark class="back">
        <v-content>
        <div>
            <v-container class="my-5">
                <v-layout row wrap>
                    <v-flex xs6>
                        <v-card-text class="justify-center" >
                            <v-btn @click="getMyBeer" class="buttonBeer">Veux tu ma bière jeune enfant</v-btn>
                        </v-card-text>
                        <v-card-text class="justify-center">
                            <input type="text" v-model="search" @keyup="filter" @emptied="getMyBeer" placeholder="Chercher une bière"/>
                        </v-card-text>
                        <v-card-text class="justify-center">

                        </v-card-text>
                    </v-flex>
                </v-layout>
            </v-container>
            <div style="padding-top: 50px">
                <div class="cadreConteneur" v-for="element in beers"
                     :key="element.id">
                    <span><span class="boldRed" style="font-weight: bold">Nom de la bière </span><span class="text"> : {{ element.name }} ({{element.abv}}°) :  </span></span>
                    <div class="cadreGrid">
                        <br>
                        <span class="boldRed"> La description voyons : </span><span class="text">{{ element.description }}</span>
                    </div>
                    <div class="cadreGrid">
                        <br>
                        <span class="boldBlue">Première fois brassée : </span><span class="text">{{ element.first_brewed }}</span>
                    </div>
                    <div class="cadreGrid">
                        <br>
                        <img class="img" v-bind:src="element.image_url">
                    </div>

                </div>
                <v-card-actions>
                    <v-btn @click="previousPage">Previous<a class="leftArrow" style="color: black"><v-icon size="50">keyboard_arrow_left</v-icon></a></v-btn>
                    <v-spacer></v-spacer>
                    <v-btn @click="nextPage">Next<a class="leftArrow"><v-icon size="50" style="color: black">keyboard_arrow_right</v-icon></a></v-btn>
                </v-card-actions>
            </div>


        </div>
        </v-content>
        <!--
        <footer>
            <p>© all copyright reserved to me and myself for me and my other me</p>
        </footer>-->
    </v-app>
</template>

<script>
    import axios from 'axios';

    /* La classe du composant API.vue */
    export default {
        data(){
            return {
                beers: [],
                search: null,
                abv_gt: null,
                brewed_before: null,
                brewed_after: null
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
            },

            previousPage() {

            },
            nextPage() {

            },

            filter() {
                let queryparams = "";
                if(this.search !== null) {
                    queryparams += "&beer_name=" + this.search
                }
                if(this.abv_gt !== null) {
                    queryparams += "&abv_gt=" + this.abv_gt
                }
                if(this.brewed_before !== null) {
                    queryparams += "&brewed_before=" + this.brewed_before
                }
                if(this.brewed_after !== null) {
                    queryparams += "&brewed_after=" + this.brewed_after
                }
                axios.get('https://api.punkapi.com/v2/beers?' + queryparams)
                    .then((beer) => {
                        console.log(beer.request.response);
                        this.beers = JSON.parse(beer.request.response)
                    })
                    .catch(() => { // function()
                            this.beers = "pas de bière";
                        }
                    )
            },
        }
        /*,
        computed: {

            {
                return this.beers.filter((blog) => {
                    return blog.name.toLowerCase().match(this.search.toLowerCase())
                })
            }
        }*/
    };
</script>
https://uigradients.com/#Memariani
<style scoped>
    .back{
        background: linear-gradient(#203A43, #2C5364);
    }
    .text{
        color: #42b983;
    }
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
        transition-duration: 0.2s;
        width: 550px;
        height: 75px;

    }
    .buttonBeer:hover{
        background-position: right center;
        background-color: black;
        border-radius: 50px;
        box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24), 0 17px 50px 0 rgba(0,0,0,0.19);
    }
    .buttonBeer:active{
        background-color: #3e8e41;
        box-shadow: 0 5px #666;
        transform: translateY(4px);
    }
    .rechercheBarre{
        position: absolute;
        top: 1.5vw;
        left: 140vh;

    }
    input{
        border: 3px solid #32e17c;
        height: 40px;
        width: 200px;
        border-radius: 50px;
        padding: 0px 10px;
        color: #203A43;
        background-color: white;
    }
    .arrow{
        bottom: 10vh;
        position: fixed;

    }
    footer{
        margin-left: auto;
        margin-right: auto;
    }
</style>