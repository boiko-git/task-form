<template>
  <div id="page">
      <checkoutForm />
  </div>
</template>
  
<script>
import checkoutForm from "~/components/checkout/CheckoutForm.vue";

export default {
  name: 'Checkout',

  components: {  
    checkoutForm
  }
}
</script>
  
