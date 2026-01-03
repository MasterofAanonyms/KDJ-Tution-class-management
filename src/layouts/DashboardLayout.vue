<template>
  <q-layout view="hHh lpR fFf" class="bg-black text-white">
    <q-header elevated class="bg-grey-10 text-white" style="border-bottom: 1px solid #333">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="text-weight-bold tracking-widest">
          KDJ<span class="text-grey-5">TUITION</span>
          <span class="text-caption text-grey-5 q-ml-sm">Dashboard</span>
        </q-toolbar-title>

        <q-btn flat round dense icon="notifications" class="q-mr-sm" />
        <q-btn flat no-caps label="Logout" icon-right="logout" @click="handleLogout" />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-black text-white"
      :width="250"
      :breakpoint="500"
      style="border-right: 1px solid #333"
    >
      <q-list padding class="text-grey-4">
        <q-item-label header class="text-grey-6 text-uppercase text-weight-bold letter-spacing-1">
          Menu
        </q-item-label>

        <q-item
          v-for="link in links"
          :key="link.text"
          clickable
          v-ripple
          active-class="text-white bg-grey-9"
          :active="link.active"
        >
          <q-item-section avatar>
            <q-icon :name="link.icon" />
          </q-item-section>

          <q-item-section>
            <q-item-label>{{ link.text }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref, inject } from 'vue'
import { useRouter } from 'vue-router'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const router = useRouter()
const supabase = inject('supabase')

const leftDrawerOpen = ref(false)

const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

const links = [
  { text: 'Dashboard', icon: 'dashboard', active: true },
  { text: 'Students', icon: 'people' },
  { text: 'Classes', icon: 'class' },
  { text: 'Teachers', icon: 'school' },
  { text: 'Payments', icon: 'payments' },
  { text: 'Settings', icon: 'settings' },
]

const handleLogout = async () => {
  try {
    const { error } = await supabase.auth.signOut()
    if (error) throw error
    router.push('/login')
    $q.notify({
      type: 'positive',
      message: 'Logged out successfully',
      position: 'top',
    })
  } catch (error) {
    console.error('Logout error:', error)
    $q.notify({
      type: 'negative',
      message: error.message || 'Error logging out',
      position: 'top',
    })
  }
}
</script>

<style lang="scss" scoped>
.letter-spacing-1 {
  letter-spacing: 1px;
}
.tracking-widest {
  letter-spacing: 2px;
}
</style>
