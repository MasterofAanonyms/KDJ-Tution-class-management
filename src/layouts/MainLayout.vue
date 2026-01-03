<template>
  <q-layout view="hHh lpR fff" class="bg-black text-white">
    <q-header :class="{ 'glass-effect': isScrolled }" class="text-white fixed-top" height-hint="98">
      <q-toolbar class="q-py-md q-px-lg">
        <q-btn flat no-caps no-wrap dense to="/" class="q-mr-sm">
          <q-avatar square size="32px" class="q-mr-sm">
            <q-icon name="school" size="28px" />
          </q-avatar>
          <q-toolbar-title shrink class="text-weight-bold tracking-widest text-h6">
            KDJ<span class="text-grey-5">TUITION</span>
          </q-toolbar-title>
        </q-btn>

        <q-space />

        <div class="gt-sm q-gutter-x-md">
          <q-btn flat no-caps label="Features" />
          <q-btn flat no-caps label="Courses" />

          <template v-if="!user">
            <q-btn
              unelevated
              color="white"
              text-color="black"
              label="Get Started Free"
              class="q-px-lg q-py-xs text-weight-bold"
              style="border-radius: 8px"
              to="/register"
            />
          </template>

          <template v-else>
            <div class="inline-block text-grey-5 q-mr-md">Hi, {{ user.email?.split('@')[0] }}</div>
            <q-btn
              unelevated
              color="white"
              text-color="black"
              label="Logout"
              class="q-px-lg q-py-xs text-weight-bold"
              style="border-radius: 8px"
              @click="handleLogout"
            />
          </template>
        </div>

        <q-btn flat icon="menu" class="lt-md" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <!-- Comprehensive Footer -->
    <footer class="bg-black text-white q-py-xl border-top-grey">
      <div class="container-limit q-mx-auto q-px-md">
        <div class="row q-col-gutter-xl">
          <div class="col-12 col-md-4">
            <div class="row items-center q-mb-md">
              <q-icon name="school" size="32px" class="q-mr-sm" />
              <span class="text-h6 text-weight-bold tracking-widest"
                >KDJ<span class="text-grey-5">TUITION</span></span
              >
            </div>
            <p class="text-grey-5" style="line-height: 1.6">
              Empowering education with advanced management tools. Streamline your institute's
              operations today.
            </p>
            <div class="row q-gutter-sm q-mt-lg">
              <q-btn round flat icon="fab fa-linkedin" size="sm" class="bg-grey-9" />
              <q-btn round flat icon="fab fa-tiktok" size="sm" class="bg-grey-9" />
              <q-btn round flat icon="fab fa-instagram" size="sm" class="bg-grey-9" />
              <q-btn round flat icon="fab fa-facebook" size="sm" class="bg-grey-9" />
            </div>
          </div>

          <div class="col-6 col-md-2">
            <div class="text-subtitle1 text-weight-bold q-mb-md">Product</div>
            <div class="flex column q-gutter-y-sm text-grey-5">
              <a href="#" class="footer-link">Features</a>
              <a href="#" class="footer-link">Pricing</a>
              <a href="#" class="footer-link">Showcase</a>
              <a href="#" class="footer-link">Changelog</a>
            </div>
          </div>

          <div class="col-6 col-md-2">
            <div class="text-subtitle1 text-weight-bold q-mb-md">Company</div>
            <div class="flex column q-gutter-y-sm text-grey-5">
              <a href="#" class="footer-link">About Us</a>
              <a href="#" class="footer-link">Careers</a>
              <a href="#" class="footer-link">Blog</a>
              <a href="#" class="footer-link">Contact</a>
            </div>
          </div>

          <div class="col-12 col-md-4">
            <div class="text-subtitle1 text-weight-bold q-mb-md">Subscribe</div>
            <p class="text-grey-5 q-mb-md">Get the latest updates and resources.</p>
            <q-input
              dark
              outlined
              dense
              placeholder="Enter your email"
              class="q-mb-sm"
              bg-color="grey-10"
            >
              <template v-slot:append>
                <q-btn flat round dense icon="arrow_forward" color="white" />
              </template>
            </q-input>
          </div>
        </div>

        <div
          class="row justify-between items-center q-mt-xl pt-lg border-top-grey-light text-grey-6 text-caption"
        >
          <div>&copy; 2024 KDJ Tution Systems. All rights reserved.</div>
          <div class="row q-gutter-x-md">
            <a href="#" class="footer-link">Privacy Policy</a>
            <a href="#" class="footer-link">Terms of Service</a>
          </div>
        </div>
      </div>
    </footer>
  </q-layout>
</template>

<script setup>
import { ref, onMounted, onUnmounted, inject } from 'vue'
import { useRouter } from 'vue-router'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const router = useRouter()
const supabase = inject('supabase')

const isScrolled = ref(false)
const user = ref(null)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

const handleLogout = async () => {
  try {
    const { error } = await supabase.auth.signOut()
    if (error) throw error
    $q.notify({
      type: 'positive',
      message: 'Logged out successfully',
      position: 'top',
    })
    // User state will automatically update via onAuthStateChange
    router.push('/')
  } catch (error) {
    $q.notify({
      type: 'negative',
      message: error.message || 'Error logging out',
      position: 'top',
    })
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  // Check current user
  supabase.auth.getUser().then(({ data }) => {
    user.value = data.user
  })

  // Listen for auth changes
  supabase.auth.onAuthStateChange((event, session) => {
    user.value = session?.user || null
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style lang="scss" scoped>
.tracking-widest {
  letter-spacing: 2px;
}
.border-top-grey {
  border-top: 1px solid #222;
}
.border-top-grey-light {
  border-top: 1px solid #222;
  padding-top: 24px;
}
.container-limit {
  max-width: 1200px;
}
.footer-link {
  color: #9e9e9e; // grey-5
  text-decoration: none;
  transition: color 0.3s;
  &:hover {
    color: white;
  }
}
.q-header {
  transition: all 0.3s ease;
  &.glass-effect {
    background: rgba(0, 0, 0, 0.5) !important;
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  }
  &:not(.glass-effect) {
    background: transparent !important; // Start transparent to blend with Hero
  }
}
</style>
