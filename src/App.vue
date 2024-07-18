<template>
  <div id="app" class="container mt-5">
    <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @toggle="toggleSliderStatus"></navbar>
    <h1>IDShop</h1>
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum"></price-slider>
    <product-list class="animate__animated animate__fadeInRight" :products="products" :maximum="maximum" @add="addItem"></product-list>
    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
    <price :value="4.90"></price>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Navbar from "./components/navbarComponent.vue";
import priceSlider from "./components/PriceSlider.vue";
import price from "./components/priceComponent.vue";
import ProductList from "./components/productList.vue";


export default {
  name: "App",
  data: function () {
  return {
    maximum: 50,
    products: [],
    cart: [],
    sliderStatus: false
  }
  },
  components: {
    FontAwesomeIcon,
    Navbar,
    priceSlider,
    price,
    ProductList,
  },
  mounted: function () {
    fetch('https://hplussport.com/api/products/order/price')
    .then(response => response.json())
    .then(data => {
      this.products = data;
    })
  },

  computed: {
    cartTotal: function () {
      let sum = 0;
      for (let key in this.cart) {
        sum = sum + (this.cart[key].product.price * this.cart[key].qty);
      }
      return sum;
    },
    cartQty: function () {
      let qty = 0;
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    }
  },

  methods: {
    toggleSliderStatus: function() {
      this.sliderStatus = !this.sliderStatus;
    },

    addItem: function(product) {
        let productIndex;
        let productExist = this.cart.filter(function(item, index) {
            if (item.product.id == Number(product.id)) {
                productIndex = index;
                return true;
            } else {
                return false;
            }
        });

        if (productExist.length) {
            this.cart[productIndex].qty++
        } else {
            this.cart.push({product: product, qty: 1});
        }
    },
  }
};
</script>
