<script setup>
import { computed } from 'vue'
const { items } = defineProps({
  items: { type: Array, required: true },
})

const emit = defineEmits(['remove-cart'])
const removeItem = (id) => emit('remove-cart', id)

const total = computed(() => items.reduce((sum, it) => sum + it.price * it.qty, 0))
</script>

<template>
  <div class="sticky-top" style="top: 24px">
    <h2 class="mb-3">購物車</h2>

    <div v-if="items.length === 0" class="text-muted text-center">購物車是空的</div>

    <div v-else>
      <div
        v-for="it in items"
        :key="it.id"
        class="d-flex justify-content-between align-items-center mb-2"
      >
        <div>
          {{ it.name }} × {{ it.qty }}
          <small class="text-muted">（NT$ {{ it.price }}）</small>
        </div>
        <button class="btn btn-outline-danger btn-sm" @click="removeItem(it.id)">刪除</button>
      </div>
      <hr />
      <div class="text-end fw-bold">總計：NT$ {{ total }}</div>
    </div>
  </div>
</template>
