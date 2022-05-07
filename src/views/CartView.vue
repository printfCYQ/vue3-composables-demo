<script setup lang="ts">
import { useCart } from "@/composables/useCart";
import { Delete } from "@element-plus/icons-vue";

const {
  cart,
  updateQuantity,
  removeFromCart,
  isCartEmpty,
  totalProducts,
  totalPrice,
} = useCart();
</script>
<template>
  <div class="cart">
    <el-card class="box-card">
      <template #header>
        <div class="card-header">
          <h1>My Cart</h1>
        </div>
      </template>
      <template v-if="isCartEmpty">
        <el-empty description="购物车空空如也" />
      </template>

      <template v-if="!isCartEmpty">
        <div v-for="item in cart.items" :key="item.productId">
          <div class="cart-item">
            <div>{{ item.name }}</div>
            <div>¥ {{ item.price }}</div>
            <el-input-number
              :modelValue="item.quantity"
              :min="0"
              @update:modelValue="(quantity: number) => updateQuantity(item, quantity)"
            ></el-input-number>
            <div>¥ {{ item.price * item.quantity }}</div>
            <el-button @click="removeFromCart(item)" :icon="Delete"></el-button>
          </div>
          <el-divider />
        </div>
      </template>
      <div v-if="!isCartEmpty" class="card-footer">
        共{{ totalProducts }}商品，¥{{ totalPrice }}
      </div>
    </el-card>
  </div>
</template>

<style>
.cart {
  margin-top: 20px;
}
.cart-item {
  display: flex;
  justify-content: space-around;
}

.card-footer {
  display: flex;
  justify-content: end;
}
</style>
