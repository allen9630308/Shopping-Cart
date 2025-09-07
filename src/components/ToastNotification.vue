<script setup>
import { inject } from 'vue'

const notification = inject('notificationState')
</script>

<template>
  <transition name="fade">
    <div
      v-if="notification?.show"
      class="alert"
      :class="{
        'alert-success': notification?.type === 'success',
        'alert-danger': notification?.type === 'danger',
        'alert-info': notification?.type === 'info',
      }"
      style="position: fixed; right: 16px; bottom: 16px; min-width: 240px; z-index: 2000"
    >
      {{ notification?.message }}
    </div>
  </transition>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
