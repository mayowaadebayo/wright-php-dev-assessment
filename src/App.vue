<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/images/logo.jpg">
    <Home msg="Welcome to Wright Auction App"/>
    <div>
      <ul>
        <li>
         <router-link to="/">
         Home
        </router-link>
        </li>
        <li>
         <router-link to="/">
         Search
        </router-link>
        </li>
        <li>
         <router-link to="/">
         About
        </router-link>
        </li>
      </ul>
      <hr/>
      <h3>Perform a search now!</h3>
      <form @submit.prevent="fetchProducts">
      
  &nbsp;
      <select required v-model="brand">
        <option>--Product brand--</option>
        <option value="colourpop">Colourpop</option>
        <option value="rejuva minerals">Rrejuva minerals</option>
      </select>
      &nbsp;
      <input type="text" placeholder="Product name" v-model="product_name"/>
      &nbsp;
      <input type="submit" value="Search now!" name="search" required/>  
      </form>    
      {{Products}}
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  },
    data () {
    return {
      Products: [],
        type:'',
        brand:'',
        product_name:''
    }
   
  },
  mounted(){
    // this.fetchUsers();
  },
  methods:{
    fetchProducts: function () {
      const baseURI = 'http://makeup-api.herokuapp.com/api/v1/products.json?brand='+this.brand+'&name='+this.product_name
      this.$http.get(baseURI)
      .then((result) => {
        this.Products = result.data
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: red;
}
</style>
