<template>
  <router-view />
</template>

<script setup>
import { Notify } from 'quasar'

// Global Notification Defaults
Notify.setDefaults({
  position: 'top',
  timeout: 3000,
  textColor: 'white',
  actions: [{ icon: 'close', color: 'grey-5', round: true, size: 'sm' }],
  progress: false, // Disable horizontal progress bar
})

// Customizing Notification Types for the "Glass" look with colored borders
Notify.registerType('positive', {
  icon: 'check_circle',
  classes: 'glass-notification border-green',
})

Notify.registerType('negative', {
  icon: 'error',
  classes: 'glass-notification border-red',
})

Notify.registerType('warning', {
  icon: 'warning',
  classes: 'glass-notification border-yellow',
})

Notify.registerType('info', {
  icon: 'info',
  classes: 'glass-notification border-blue',
})
</script>

<style lang="scss">
// Global Notification Styles
.glass-notification {
  background: rgba(10, 10, 10, 0.85) !important; // Darker, more opaque background
  backdrop-filter: blur(16px) !important;
  border: 1px solid rgba(255, 255, 255, 0.08) !important;
  border-radius: 12px !important;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.6) !important;
  color: white !important;
  min-width: 320px;
  position: relative;
  overflow: hidden; // Ensures the line stays inside the rounded corners
  padding-left: 24px !important; // Add space for the content away from the line
}

// The Vertical Line Indicator using pseudo-element
.glass-notification::before {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  width: 6px;
  z-index: 1;
}

// Indicator Colors & Glow effects
.border-green::before {
  background: #4caf50;
  box-shadow: 2px 0 15px rgba(76, 175, 80, 0.6); // Green glow
}

.border-red::before {
  background: #f44336;
  box-shadow: 2px 0 15px rgba(244, 67, 54, 0.6); // Red glow
}

.border-yellow::before {
  background: #ffc107;
  box-shadow: 2px 0 15px rgba(255, 193, 7, 0.6); // Yellow glow
}

.border-blue::before {
  background: #2196f3;
  box-shadow: 2px 0 15px rgba(33, 150, 243, 0.6); // Blue glow
}
</style>
