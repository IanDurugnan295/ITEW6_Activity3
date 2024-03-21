<template>
    <div class="products">
      <table style="width:40%; table-layout: fixed;" align="center">
        <th>Product Name</th>
        <th>Price</th>
        <th>Button</th>
        <tr v-for="item in products" :key="item.id">
          <td>{{ item.name }}</td>
          <td align="right">₱{{ item.price }}.00</td>
          <td><button @click="addToCart(item)">Add to Cart</button></td>
        </tr>
      </table>
    </div>
  </template>
  
  <script>
  import { cart } from "../main.js";
  
  export default {
    data() {
      return {
        products: [
          { name: "Choco Mucho", price: 20 },
          { name: "Stick O", price: 50 },
          { name: "Choc O", price: 35 },
          { name: "Bear Brand", price: 12 },
          { name: "Milo", price: 11 },
          { name: "Energen", price: 12 },
          { name: "Choo Choo", price: 60 },
          { name: "Cheesecake", price: 65 },
          { name: "Nissin Wafer", price: 55 },
          { name: "Potato Chips", price: 25 }
        ],
      };
    },
    methods: {
      addToCart(item) {
        let existingItemIndex = cart.findIndex(cartItem => cartItem.name === item.name);

        if (existingItemIndex !== -1) {
          let answer = prompt("How many pieces?", "Please enter the amount");
          if (answer == null || answer === "") {
            alert("User cancelled the prompt!");
            return;
          }
          cart[existingItemIndex].quantity += parseInt(answer);
        } else {
          let answer = prompt("How many pieces?", "Please enter the amount");
          if (answer == null || answer === "") {
            alert("User cancelled the prompt!");
            return;
          }
          
          let totalPrice = item.price * answer;
          cart.push({
            name: item.name,
            price: totalPrice,
            unitPrice: item.price,
            quantity: parseInt(answer)
          });
        }
      },
      handleLogout() {
        localStorage.removeItem('token');
        this.$router.push('/login');
      }
    },
  };
  </script>
  
  <style>
  table, th, td {
    border:1px solid black;
  }
  </style>
  