<script setup lang="ts">
import { useCart } from "@/composables/useCart";
import { onMounted, ref } from "vue";

import { ShoppingCart } from "@element-plus/icons-vue";

const { addToCart } = useCart();

const products = ref<Product[]>([]);
onMounted(() => {
  products.value = [
    {
      id: 1,
      name: "Product 1",
      price: 10,
    },
    {
      id: 2,
      name: "Product 2",
      price: 20,
    },
    {
      id: 3,
      name: "Product 3",
      price: 30,
    },
  ];
});
</script>

<template>
  <div class="products">
    <el-card class="box-card">
      <template #header>
        <div class="card-header">
          <h1>Products List</h1>
        </div>
      </template>
      <div v-for="product in products" :key="product.id">
        <div class="products-item">
          <div>{{ product.name }}</div>
          <div>¥ {{ product.price }}</div>
          <span> </span>
          <el-button
            class="btn"
            type="primary"
            @click="addToCart(product)"
            :icon="ShoppingCart"
          ></el-button>
        </div>
        <el-divider />
      </div>
    </el-card>
  </div>
</template>
<style>
.products {
  margin-top: 20px;
}
.products-item {
  display: flex;
  justify-content: space-around;
}
</style>
