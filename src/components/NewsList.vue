<template>

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
</template>

<script>


export default {

    data() {

        return {

            articles: []

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