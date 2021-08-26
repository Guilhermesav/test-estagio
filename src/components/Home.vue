<template>
  <div id = "lista">
    <h1>Hacker news</h1> 
    <div id = "noticias"> 
    <ul class ="itens" v-for="news in newsList" :key="news.id">
          <li> "{{news.title}}" by {{news.by}} Score: {{news.score}}</li>
    </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
    name: 'Home',
    data(){
        return{
            newsList : []
        };
    },
    created(){
        for(let i =0;i<10;i++){
            axios.get("https://hacker-news.firebaseio.com/v0/topstories.json?print=pretty").then((response) => {
            return axios.get(`https://hacker-news.firebaseio.com/v0/item/${response.data[i]}.json?print=pretty`);
            }).then((response) => {this.newsList.push(response.data)});
        }
    }
}
</script>

<style>
#lista{

    text-align: center;
}
#noticias{
    background-color: antiquewhite;
    border:1px solid;
    border-radius: 25px;
    text-align: center;
    
}
.itens{
    border:1px none ;
    box-shadow: 1px 1px black;
}
</style>