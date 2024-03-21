<template>
  <div class="cart">
    <table style="width:40%; table-layout: fixed;" align="center">
      <th>Product Name</th>
      <th>Price</th>
      <th>Quantity</th>
      <th>Edit</th>
      <th>Remove</th>
      <tr v-for="(item, index) in cart" :key="index">
        <td>{{ item.name }}</td>
        <td align="right">₱{{ item.price }}.00</td>
        <td align="right">{{ item.quantity }}</td>
        <td><button @click="editQuantity(index)">Edit Quantity</button></td>
        <td><button @click="removeFromCart(index)">Remove from Cart</button></td>
      </tr>
    </table>
      <div class="checkout">
        <p>Total Price: ₱{{ totalPrice }}</p>
        <button @click="checkOut()">Check Out</button>
      </div>
  </div>
</template>

<script>
import { cart } from "../main.js";

export default {
  data() {
    return {
      cart: cart,
    };
  },
  methods: {
    removeFromCart(index) {
      if (confirm("Are you sure you want to remove this item from the cart?")) {
        this.cart.splice(index, 1);
      }
    },
    editQuantity(index) {
        const newQuantity = prompt("Enter the new quantity:", this.cart[index].quantity);
        let unitPrice = this.cart[index].price / this.cart[index].quantity;
        if (newQuantity !== null && !isNaN(newQuantity) && newQuantity > 0) {
          this.cart[index].price = unitPrice * newQuantity;
          this.cart[index].quantity = parseInt(newQuantity);
        }
    },
    checkOut(){
      alert("Check Out is not part of the task!")
    }
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + parseInt(item.price), 0);
    }
  }
};
</script>

<style>
table, th, td {
  border: 1px solid black;
}
</style>
