<script>
    import axios from 'axios';

    export default {
        data(){
            return{
                query: '',                                                 // dichiaro una stringa

                arrayFilm: [],
                arraySerieTv: [],

                API_KEY:'95fdb4551d221f480fcc3d8ca84aaec4',                // nomino come parametro la mia key per poterla riutilizzare
            }
        },

        methods: {
            serverResponse(){
                axios.get('https://api.themoviedb.org/3/search/movie',{    // interrogo l'API sui vari film
                    params:{                                               // nomino i parametri da inserire oltre alla stringa già scrita
                        api_key: this.API_KEY,                             // dico quale parametro inserire
                        query: this.query,                                 // inserisco tra i parametri anche una stringa come parametro di ricerca
                    }
                })
                .then((result1) => {
                    for(let i = 0; i < 20; i++){
                        this.arrayFilm.push(result1.data.results[i].title)
                        this.arrayFilm.push(result1.data.results[i].original_title)
                        this.arrayFilm.push(result1.data.results[i].original_language)
                        this.arrayFilm.push(result1.data.results[i].vote_average)
                        this.arrayFilm.push(result1.data.results[i].overview)
                        this.arrayFilm.push(result1.data.results[i].poster_path)
                    }
                    console.log(this.arrayFilm)
                })

                axios.get('https://api.themoviedb.org/3/search/tv',{      // interrogo l'API sui vari film
                    params:{                                              // nomino i parametri da inserire oltre alla stringa già scrita
                        api_key:this.API_KEY,                             // dico quale parametro inserire
                        query: this.query,                                // inserisco tra i parametri anche una stringa come parametro di ricerca
                    }
                })
                .then((result2) => {
                    for(let i = 0; i < 20; i++){
                        this.arraySerieTv.push(result2.data.results[i].name)
                        this.arraySerieTv.push(result2.data.results[i].original_name)
                        this.arraySerieTv.push(result2.data.results[i].original_language)
                        this.arraySerieTv.push(result2.data.results[i].vote_average)
                        this.arraySerieTv.push(result2.data.results[i].overview)
                        this.arraySerieTv.push(result2.data.results[i].poster_path)
                    }
                    console.log(this.arraySerieTv)
                })
            }
        }
    }
</script>

<template>
    <div>
        <input type="text" v-model="query">
        <button @click="serverResponse()">cerca</button>
    </div>
</template>

<style scoped>

</style>