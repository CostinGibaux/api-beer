<template>
    <v-app dark class="back">
        <!--// La balise qui content le header/body/footer de mon application-->
        <v-content>
            <!--// La div qui contient l'ensemble de l'app-->
            <div>
                <!--// Dans cette div il y a les 4 barres de recherche-->
                <v-container class="my-5">
                    <v-layout row wrap>
                        <v-flex xs20>
                            <v-card-text class="justify-center">
                                <!--// La barre de recherche du nom-->
                                <input type="text" v-model="search" @keyup="filter" @emptied="getMyBeer" placeholder="Nom"/>
                            </v-card-text>
                        </v-flex>
                        <v-flex xs20>
                            <v-card-text class="justify-center">
                                <!--// La barre de recherche pour filter par rapport au degré d'alcool-->
                                <input type="text" v-model="abv_gt" @keyup="filter" @emptied="getMyBeer" placeholder="ABV > à"/>
                            </v-card-text>
                        </v-flex>
                        <v-flex xs20>
                            <v-card-text class="justify-center">
                                <!--// La barre de recherche pour savoir avant quelle année la bière a été brassée-->
                                <input type="text" v-model="brewed_before" @keyup="filter" @emptied="getMyBeer" placeholder="brassée avant"/>
                            </v-card-text>
                        </v-flex>
                        <v-flex xs20>
                            <v-card-text class="justify-center">
                                <!--// La barre de recherche pour savoir après quelle année la bière a été brassée-->
                                <input type="text" v-model="brewed_after" @keyup="filter" @emptied="getMyBeer" placeholder="brassée après"/>
                            </v-card-text>
                        </v-flex>
                    </v-layout>
                </v-container>
            </div>
            <div style="padding-top: 50px">
                <!--Cette div contient le reste de la page c'est à dire les renseignement sur les bières ainsi que les boutons pour changer de page-->
                <div class="cadreConteneur" v-for="element in beers"
                     :key="element.id">
                    <!--La boucle for pour faire apparaître les bières-->
                    <span><span class="boldRed" style="font-weight: bold">Nom de la bière </span><span class="text"> : {{ element.name }} ({{element.abv}}°) :  </span></span>
                    <!--Le nom de la bière-->
                    <div class="cadreGrid">
                        <br>
                        <span class="boldRed"> La description voyons : </span><span class="text">{{ element.description }}</span>
                        <!--La description de la bière-->
                    </div>
                    <div class="cadreGrid">
                        <br>
                        <span class="boldBlue">Première fois brassée : </span><span class="text">{{ element.first_brewed }}</span>
                        <!--La première fois que la bière en question a été brassée-->
                    </div>
                    <div class="cadreGrid">
                        <br>
                        <img class="img" v-bind:src="element.image_url">
                        <!--L'image de la bière qui va bien-->
                    </div>
                </div>
                <v-card-actions>
                    <v-btn @click="previousPage">Previous<a class="leftArrow" style="color: black"><v-icon size="50">keyboard_arrow_left</v-icon></a></v-btn>
                    <!--Le bouton de la flèche qui permet de revenir en arrière dans les pages-->
                    <v-spacer></v-spacer>
                    <v-btn @click="nextPage">Next<a class="leftArrow"><v-icon size="50" style="color: black">keyboard_arrow_right</v-icon></a></v-btn>
                    <!--Le bouton qui permet de changer de page pour voir ce qu'il y a après-->
                </v-card-actions>
            </div>
        </v-content>
    </v-app>
    <!--Fin du front de l'app-->
</template>

<script>
    // Import de axios dans le projet pour l'appel d'API
    import axios from 'axios';

    // La classe du composant API.vue
    export default {
        data(){
            return {
                // Return les bières, les filtres de la recherche ainsi que le composant permettant de changer de page
                beers: [],
                search: null,
                abv_gt: null,
                brewed_before: null,
                brewed_after: null,
                page: 1
            }
        },
        methods: {
            // GetMyBeer est une fonction qui permet d'appeler l'API (et qui ajoute this.page pour faire fonctionner la fonction gérant les pages)
            getMyBeer() {
                axios.get('https://api.punkapi.com/v2/beers?page=' + this.page)
                    .then((beer) => {
                        // On utilise console.log en cas de problèmes
                        console.log(beer.request.response);
                        this.beers = JSON.parse(beer.request.response)
                    })
                    .catch(() => { // function()
                        // Si un problème survient
                            this.beers = "pas de bière";
                        }
                    )
            },

            previousPage() {
                // Permet de faire marcher le bouton page : Previous
                if(this.page > 1) {
                    this.page--;
                    // -- pour revenir en arrière
                }
                this.getMyBeer();
                this.scrollToTop();
                // la fonction scrollToTop permet, après avoir appuyer sur le bouton "Previous", de revenir tout en haut de la page pour éviter de devoir scroller tout en haut
            },
            nextPage() {
                // Permet de faire marcher le bouton page : Next
                this.page++;
                // ++ pour aller en avant
                this.getMyBeer();
                this.scrollToTop();
                // la fonction scrollToTop permet, après avoir appuyer sur le bouton "Next", de revenir tout en haut de la page pour éviter de devoir scroller tout en haut
            },

            filter() {
                // Ceci est la fonction qui permet de faire fonctionner les barres de recherche
                let queryparams = "";
                // La variable "queryparams" qui va faire varier l'url de l'api pour affiner la recherche en fonction de ce que a tapé l'utilisateur
                if(this.search !== null) {
                    queryparams += "&beer_name=" + this.search
                    // "&beer_name=" Pour chercher le nom de la bière
                }
                if(this.abv_gt !== null) {
                    queryparams += "&abv_gt=" + this.abv_gt
                    // "&abv_gt=" Chercher le degré d'alcool
                }
                if(this.brewed_before !== null) {
                    queryparams += "&brewed_before=" + this.brewed_before
                    // "&brewed_before=" Chercher les bières brassées avant
                }
                if(this.brewed_after !== null) {
                    queryparams += "&brewed_after=" + this.brewed_after
                    // "&brewed_after=" Chercher les bières brassées après
                }
                // On appel de nouveau l'api afin de prendre en compte les changement qu'a fait l'utilisateur en utilisant la barre de recherche
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
            scrollToTop() {
                // La fonction pour remonter en haut de la page
                window.scrollTo(0,0);
            }
        },
        mounted: function() {
            this.getMyBeer();
        }
    };
</script>
<!--Site de couleur pour vos sites : https://uigradients.com/#Memariani-->
<style scoped>
    .back{
        /*background: linear-gradient(#203A43, #2C5364);*/
        background: #2C5364;
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
        width: 300px;
        border-radius: 50px;
        padding: 0px 10px;
        color: #203A43;
        background-color: white;
    }
    .arrow{
        bottom: 10vh;
        position: fixed;

    }
    footer {
        margin-left: auto;
        margin-right: auto;
    }
    input:hover{
        transition: width 0.2s ease-out;
        width: 500px;
    }
</style>