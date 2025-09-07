<script setup>
import ProductList from './components/ProductList.vue'
import Cart from './components/MyCart.vue'
import Notification from './components/ToastNotification.vue'
import { ref, computed, provide, reactive } from 'vue'

const products = ref([
  {
    id: 1,
    name: '耳罩式藍牙耳機',
    description: '舒適配戴，支援降噪技術',
    price: 2490,
    image:
      'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&w=2065&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 4,
    name: '耳罩式彩虹耳機',
    description: '舒適配戴，支援降噪技術',
    price: 1380,
    image:
      'https://images.unsplash.com/photo-1524678606370-a47ad25cb82a?q=80&w=2069&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 5,
    name: '時尚藍牙耳機',
    description: '舒適配戴，支援降噪技術',
    price: 7990,
    image:
      'https://images.unsplash.com/photo-1628116709703-c1c9ad550d36?q=80&w=2071&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 2,
    name: '機械式鍵盤',
    description: '紅軸機械鍵盤，打字手感極佳',
    price: 1890,
    image:
      'https://images.unsplash.com/photo-1595044426077-d36d9236d54a?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 3,
    name: '無線滑鼠',
    description: '靜音按鍵設計，長效電池',
    price: 890,
    image:
      'https://images.unsplash.com/photo-1527814050087-3793815479db?q=80&w=1928&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
])

const cartMap = ref(new Map())
const cartItems = computed(() => Array.from(cartMap.value.values()))

const handleAddCart = (p) => {
  const existed = cartMap.value.get(p.id)
  if (existed) existed.qty += 1
  else cartMap.value.set(p.id, { ...p, qty: 1 })
  showNotification(`已加入購物車`, 'success')
}

const handleRemoveCart = (id) => {
  cartMap.value.delete(id)
  showNotification(`已移除自購物車`, 'danger')
}

const notificationState = reactive({
  show: false,
  type: 'success',
  message: '',
})
let hideTimer = null
const showNotification = (msg, type = 'success', duration = 2000) => {
  notificationState.message = msg
  notificationState.type = type
  notificationState.show = true
  if (hideTimer) clearTimeout(hideTimer)
  hideTimer = setTimeout(() => (notificationState.show = false), duration)
}
provide('notificationState', notificationState)
provide('showNotification', showNotification)
</script>

<template>
  <div class="container py-4 px-4">
    <h2>商品列表</h2>
    <div class="row">
      <div class="col-8">
        <ProductList :products="products" @add-cart="handleAddCart" />
      </div>
      <div class="col-4">
        <Cart :items="cartItems" @remove-cart="handleRemoveCart" />
      </div>
    </div>
    <Notification />
  </div>
</template>

<style>
body {
  background: #f2f2f2f2;
}

.card-img-top {
  height: 150px;
  object-fit: cover;
}
</style>
