<!--order form-->
<template>
  <div class="container">
    <h1>Place your Order</h1>
    <form class="container" onsubmit="checkout()">
        <div class="cocktails" id="column">
            <h4>Cocktails</h4>
            <ul v-for="item in Cocktails" :key="item">
              <button class="cartButton" type="button" @click="addToCart(item)">Add</button>  
              <li>{{item}} </li>
            </ul>
        </div>
        <div class="beers" id="column">
            <h4>Beers</h4>
            <ul v-for="item in Beers" :key="item">
              <button class="cartButton" type="button" @click="addToCart(item)">Add</button>  
              <li>{{item}} </li>
            </ul>
        </div>
        <div class="wines" id="column">
            <h4>Wines</h4>
            <ul v-for="item in Wines" :key="item">
              <button class="cartButton" type="button" @click="addToCart(item)">Add</button>  
              <li>{{item}} </li>
            </ul>
        </div>
        <div class="cart" id="column">
          <h4>Your Cart:</h4>
          <br />
          <p v-for="item in cart" v-bind:key="item" >
            {{item}} 
            <button class="cartButton" type="button" @click="removeFromCart(item)">x</button>
          </p>
          <button id="orderButton" v-on:click="checkout">Place Order</button>
        </div>
    </form>    
  </div>
</template>

<script>
import PostService from '../PostService.js';

export default {
  name: 'PostComponent',
  data() {
    return {
      cart : [],
      cartItems: '',
      displayCart:'',
      Cocktails:['Moscow Mule', 'Vodka Soda', 'Gin and Tonic', 'Mojito', 'Margarita', 'Daiquiri', 'Whiskey Sour'],
      Beers:['Blue Moon', 'Budweiser', 'Michelob Ultra', 'Yuengling', 'Shock Top', 'Samuel Adams', 'Modelo'],
      Wines:['Roselland Riesling', 'Blackstone Merlot', 'Maison no 9 Rose', "Chateu Chardonnay", 'Meiomi Pinot Noir', 'Barefoot Merlot', 'Barefoot Moscato'],
    }
  },
  methods: {
    addToCart(id) {
      this.cart.push(id);
      return true;
    },
    removeFromCart(id){
      console.log(id);
      for(var i = 0;i<this.cart.length;i++){
        if(this.cart[i] === id){
          if(confirm('Are you sure you want to remove '+id+' from your cart?')){
            this.cart = this.cart.filter(cart => cart !== id);
          }
        }
      }
    },
    async checkout(){
      await PostService.insertPost(this.cart);
      this.post = await PostService.getPosts();
      alert('Order has been placed');
    },
    
  }
}

</script>

<style scoped>
    .column::after {
        content: "";
        display: table;
        clear: both;
    }
   
    .cocktails {
        float: left;
        width: 22%;
    }
    .beers {
        float: left;
        width: 22%;
    }

    .wines {
        float: left;
        width: 26%;
    }
    .cartButton{
      float: left;
      position:relative;
    }
    .cart{
        float:right;
        width: 20%;
        border:5px;
        border-color:gray;
        border-style: ridge;
        text-align:center;
    }
    h1{
      width:100%;
    }
    #orderButton{
      align-content: center;
    }
</style>