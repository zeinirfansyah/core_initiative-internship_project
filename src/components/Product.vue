<template>
  <div>
    <h2>Zein Irfansyah</h2>
    <h3>Final Project Virtual Internship</h3>
    <div v-if="loading" class="loader"></div>
    <div v-else>
      <div
        :class="[
          'product-card',
          product.category === 'men\'s clothing' ? 'men' : 'women',
        ]"
      >
        <h2>{{ product.title }}</h2>
        <p>{{ product.category }}</p>
        <p>{{ product.description }}</p>
        <img :src="product.image" :alt="product.title" />
        <button class="buy" @click="getProduct">Get Product</button>
        <button class="next" @click="getNextProduct">Next Product</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      product: {},
      currentIndex: 1,
    };
  },
  created() {
    this.getProduct();
  },
  methods: {
    getProduct() {
      this.loading = true;
      fetch(`https://fakestoreapi.com/products/${this.currentIndex}`)
        .then((response) => response.json())
        .then((data) => {
          this.product = data;
          this.loading = false;
        })
        .catch((error) => {
          console.error("Error:", error);
          this.loading = false;
        });
    },
    getNextProduct() {
      this.currentIndex++;
      if (this.currentIndex > 20) {
        this.currentIndex = 1;
      }
      this.getProduct();
    },
  },
};
</script>
