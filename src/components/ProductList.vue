<script setup>
const { products } = defineProps({
  products: { type: Array, required: true },
})

const emit = defineEmits(['add-cart'])
const add = (p) => emit('add-cart', p)
</script>

<template>
  <div class="row g-3">
    <div v-for="p in products" :key="p.id" class="col-md-4">
      <div class="card h-100">
        <img
          :src="p.image"
          :alt="p.name"
          class="card-img-top"
          style="object-fit: cover; height: 140px"
        />
        <div class="card-body d-flex flex-column">
          <h6 class="card-title mb-1">{{ p.name }}</h6>
          <small class="text-muted mb-2">{{ p.description }}</small>
          <div class="fw-bold mb-2">NT$ {{ p.price }}</div>

          <button class="btn btn-primary mt-auto" @click="add(p)">加入購物車</button>
        </div>
      </div>
    </div>
  </div>
</template>
