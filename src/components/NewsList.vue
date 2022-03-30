<template>

    <form @submit.prevent ="searchNews" class="d-flex flex-column justify-content-center">
    <div class="input-group mx-sm-3 mb-2">
    <label class="visually-hidden" for="search">Search</label>
    <input type="search" name="search" v-model="searchTerm"
    id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
    Search Term Here" />
    <button class="btn btn-primary mb-2">Search</button>
    </div>
    <p>You are searching for {{ searchTerm }}</p>

    <ul class="class news__list ">
        <li v-for =" article in articles" class="news__item">
    <div class="card">
        <img class = "card-image-top" :src = "article.urlToImage">
        <div class="card-body">
            <div class="card-title">{{article.title}}</div>
            <div class="card-text">{{article.description}}</div>
        </div>
    </div>
    </li>
    

</ul>
</form>
</template>

<script>


export default {

    data() {

        return {

            articles: [],   
            searchTerm: ''

        };
    },
    created(){

        let self = this;

        fetch('https://newsapi.org/v2/top-headlines?country=us',
    {

    headers:{

        'Authorization': 'Bearer 352457c32f544ddbb6aa9eea265874f2'
    }
    })
    .then (function(response){
        return response.json();
    })

    .then(function(data){
        self.articles = data.articles
    });
    },

    methods:{
        searchNews(){

            let self = this
            fetch('https://newsapi.org/v2/everything?q='+ self.searchTerm + '&language = en',{

            headers: {

            'Authorization': 'Bearer 352457c32f544ddbb6aa9eea265874f2'

            }
            })
            .then(function(response){
                return response.json();
            })
            .then(function(data){
                console.log(data);
                self.articles = data.articles;
            });
        }
        }
    }


</script>

<style scoped>

.news__list{

	display:grid;
	grid-template-columns: auto auto auto;
    list-style: none;
    gap:20px;

}

img {

max-width:100%;
height:220px;

}


.card {

    text-align: left;
}

.card-title{

    font-weight: bold;
}


.card-body{

    height :250px;
    border-bottom: 5px solid rgb(2, 199, 2);
}
</style>