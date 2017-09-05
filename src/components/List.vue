<template>
<div>
<h4 class="text-center">Movie Database</h4><br/>
<div class="input-group">
    
    <b-form-input v-model="search"
                  type="text"

                  class="form-inline"
                  placeholder="Enter a movie name"
                  ></b-form-input>
                  <span class="input-group-btn">    
                  <b-button variant="primary" v-on:click="getPosts">Search</b-button></span>
</div>

<div class="cont">
    <i  v-show="loading" class="text-center fa fa-2x fa-spinner fa-spin"></i>
<h5 v-if="err">Not found.</h5>
    <ul v-else>
      <li v-for="post in posts.results">
            <router-link :to="{ name: 'post', params: { id: post.id }}">
               <h5>{{post.title}} </h5> 
            </router-link>
        </li>
    </ul>
    
</div>
   
</div>
</template>

<script>
var query =" ";
var api="Enter your api"
const baseUrl = "https://api.themoviedb.org/3/search/movie?api_key="+api+"&query=";
export default {
   template: '#list-template',

    data: () => ({
        posts: [],
         search: "",
         err: "",
          loading: false
    }),
  
    computed: {
        // filteredPosts() {
        //   return this.posts.filter(post => {
        //      return post.title.includes(this.search);
        //   })
        // }
      
    },
    methods: {
        getPosts(){
            this.loading=true;
            var query= this.search;
            axios.get(baseUrl+ query).then(response => {
                  this.loading=false;
                this.err="";
                this.posts = response.data
                console.log(this.posts);
                if(this.posts.total_results<=0){
                this.err="Not found"
                    
                }
                   console.log(response.status);
           
            }).catch(error => {
                this.err="Not found"
                console.log(this.posts);
                // this.errors.push(error)
                
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
.inline{
    display: inline-block;
}
.form-control{
    display: inline-block;
}
ul {
  list-style-type: none;
  padding: 0;
  
}
.cont{
    background: #f9f9f9;
    margin: 50px 0;
    padding: 20px 10px;
    text-align: left;
}
.btn.btn-primary{
    display: inline-block;
}

</style>
