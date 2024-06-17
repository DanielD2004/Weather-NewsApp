<template>
  <div id="main" >
    <input id="searchBar" placeholder="Enter a topic" @keypress="getNews" v-model="search" type="text">
    <div  id="news" v-if="typeof news.articles != 'undefined'">
      <ul ref="newsList">
        <li v-for="story in stories">
          <div id=title>
            {{ story.title }}<br/>
          </div>
          By: {{ story.author }}<br/>
          Read about it here! <a :href="story.url" target="_blank">{{ story.url }}</a><br/><br/><br/>
          <img :src="story.urlToImage">
          <hr>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            apiKey: "738662c8bc9149b0b348ebd40c99c48e",
            url: "https://newsapi.org/v2/everything",
            rank: "popularity",
            news: {},
            search: "",
            stories:[],
            list:[]
        }
    },
    methods:{
        getNews (press) {
          if (press.key == "Enter") {
            this.stories = []
            fetch(`${this.url}?q=${this.search}&sortBy=${this.rank}&apiKey=${this.apiKey}`)
            .then(data => {
              return data.json();
            }).then(this.setResponse);
            this.search = ""
          }
        },
        setResponse(response){
          this.news = response
          this.getTopStories()
      },
      getTopStories(){
        var j = 4;
        for (var i = 0; i < j; i++){
          if (this.news.articles[i].author != null){
            this.stories.push(this.news.articles[i])
          }
          else{
            j++;
          }
        }
      },
    },
    computed(){

    }
}

</script>
<style scoped>
    #main{
      background-image: linear-gradient(blue, red);
      padding:30px;
      text-align:center;
      width:75vw;
      height:100vh;
      margin:-8px;
    }

    #searchBar{
      height:50px;
      width:25vw;
      margin-bottom:20px;
      margin-top:75px;
      border-radius:0 50px 0 50px;
      padding:10px;
    }

    li{
      color:white;
    }
    #title{
      font-size:20px;
      color:white;
      font-weight:bold;
    }

    a{
      background-color: white;
      color:blue;
    }

    img{
      aspect-ratio: 1;
      height:110px;
    }
</style>