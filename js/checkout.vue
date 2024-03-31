<template>
  <div>
    <!-- Display cart items -->
    <div v-if="cart.length === 0">
      <p>Your cart is empty.</p>
    </div>
    <div v-else>
      <div v-for="cartItem in cart" :key="cartItem.id">
        <div>
          <img :src="cartItem.image" alt="" width="100" height="90">
        </div>
        <div>
          <p>{{ cartItem.subject }}</p>
          <p>{{ 'Location: ' + cartItem.location }}</p>
          <p>{{ 'Price: ' + cartItem.price }}</p>
          <p>{{ 'Spaces: ' + cartItem.spaces }}</p>
          <!-- Button to remove item from cart -->
          <button @click="removeFromCart(cartItem.id)">Remove</button>
        </div>
      </div>
    </div>
    <br>
    <!-- Checkout form -->
    <form id="checkoutForm">
      <input type="text" id="name" placeholder="Enter your Name" pattern="[A-Za-z ]+" required v-model="order.firstName">
      <input type="tel" id="phone" placeholder="Enter your Phone number" pattern="[0-9]+" required v-model="order.lastName">
      <!-- Button to trigger checkout -->
      <button @click="checkout" :disabled="!isCheckoutEnabled">Checkout</button>
      <!-- Display message after successful order submission -->
      <p v-if="orderSubmitted">Order submitted!</p>
    </form>
  </div>
</template>

<script>
export default {
  props: ['cart'],
  data() {
    return {
      order: {
        firstName: '',
        lastName: ''
      },
      orderSubmitted: false
    };
  },
  methods: {
    removeFromCart(itemId) {
      // Emit an event to notify the parent component to remove the item from the cart
      this.$emit('remove-from-cart', itemId);
    },
    checkout() {
      // Implement the checkout logic
      // Set orderSubmitted to true after successful checkout
      this.orderSubmitted = true;
    },
    isCheckoutEnabled() {
      // Implement the logic to determine if checkout button should be enabled
      // For example, check if order details are filled
      return this.order.firstName && this.order.lastName;
    }
  }
}
</script>

<style scoped>
/* Add your component-specific styles here */
</style>
