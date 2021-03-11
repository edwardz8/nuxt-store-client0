<template>
  <div class="container">
    <h1 class="title">
      nuxt digital assets commerce

      <FeaturedProduct />

      <!-- <div v-for="product in products" :key="product._id">
        <b-card>
          <b-card-title>{{ product.name }}</b-card-title>
          <p>{{ product.owner.name }}</p>
        </b-card>
        </div> -->
    </h1>
  </div>
</template>

<script>
import FeaturedProduct from '@/components/FeaturedProduct'

export default {
  components: {
    FeaturedProduct
  },
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get('/api/products')
        console.log(response)

      return {
        products: response.products
      }
    } catch (err) {
      console.log(err)
    }
  },
  data() {
    return {
      products: []
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 600;
  font-size: 30px;
  letter-spacing: 1px;
}

.links {
  padding-top: 15px;
}
</style>
