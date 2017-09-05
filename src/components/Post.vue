<template>

   <div>
        <router-link :to="{ name: 'homepage' }">Homepage</router-link>
 <i  v-show="loading" class="fa fa-2x fa-spinner fa-spin"></i>
  <div class="row">
    <div class="col-md-6 text-center">
  <b-card :title="post.title"
          :img-src="'https://image.tmdb.org/t/p/w300_and_h450_bestv2/'+post.poster_path"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2"></b-card>      
    </div>   <div class="col-md-6">
        

    <p class="txt text-left">
      
        {{post.overview}}<br/>
        <b>Genre :   <span v-for="genre in post.genres">
            {{genre.name}}, 
        </span></b><br/>
       <b>Runtime :    {{post.runtime}} minutes</b><br/>
       <b>Release Date : {{post.release_date}}</b>

    </p>
   <router-link class="white" :to="{ name: 'homepage' }">  
       <b-button variant="primary" class="white">Back</b-button>
    
    </router-link>
 
    </div> 
  </div>
 

    </div>
</template>

<script>
const baseUrl = "https://api.themoviedb.org/3/movie/"
const api= "?api_key=Enter your api";
export default {
     template: '#post-template',
    data: () => ({
        post: null,
          loading: false
    
    }),
    mounted() {
        this.getPosts();
    },
    methods: {
        getPosts(){
            this.loading=true;
          var id = this.$route.params.id;
            axios.get(baseUrl +id+api).then(response => {
                this.loading=false;
                this.post = response.data;
            
                console.log(this.post);
            }).catch(error => {
                console.log(error);
            })
        }
    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
.white{
    color: #fff !important; 
}
.card {
        margin: 0 auto; /* Added */
        float: none; /* Added */
        margin-bottom: 10px; /* Added */
}
.txt{
    margin: 50px 0;
}
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}


</style>
