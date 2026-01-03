<template>
  <q-page class="bg-black text-white flex flex-center relative-position overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute-full overflow-hidden">
      <!-- Gradient Fade similar to Home -->
      <div class="absolute-full bg-gradient-fade"></div>

      <!-- Decorative blurred circle -->
      <div
        class="absolute-top-right bg-white"
        style="
          width: 300px;
          height: 300px;
          border-radius: 50%;
          opacity: 0.1;
          filter: blur(80px);
          transform: translate(30%, -30%);
        "
      ></div>

      <div
        class="absolute-bottom-left bg-white"
        style="
          width: 400px;
          height: 400px;
          border-radius: 50%;
          opacity: 0.05;
          filter: blur(100px);
          transform: translate(-30%, 30%);
        "
      ></div>
    </div>

    <!-- Login Card -->
    <div class="relative-position z-top" style="width: 100%; max-width: 400px; padding: 20px">
      <div class="text-center q-mb-xl">
        <q-icon name="school" color="white" size="48px" class="q-mb-md" />
        <div class="text-h4 text-weight-bold">Welcome Back</div>
        <div class="text-grey-5 q-mt-sm">Sign in to manage your institute</div>
      </div>

      <q-card
        class="bg-grey-10 text-white shadow-24"
        style="border-radius: 24px; border: 1px solid #333"
      >
        <q-card-section class="q-pa-lg q-pa-md-xl">
          <q-form @submit="handleLogin" class="q-gutter-y-lg">
            <div>
              <label
                class="text-grey-5 q-mb-sm block text-caption text-uppercase text-weight-bold tracking-wider"
                >Email Address</label
              >
              <q-input
                dark
                borderless
                dense
                v-model="email"
                placeholder="john@example.com"
                class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                type="email"
                :rules="[(val) => !!val || 'Email is required']"
              />
            </div>

            <div>
              <label
                class="text-grey-5 q-mb-sm block text-caption text-uppercase text-weight-bold tracking-wider"
                >Password</label
              >
              <q-input
                dark
                borderless
                dense
                v-model="password"
                placeholder="••••••••"
                class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                type="password"
                :rules="[(val) => !!val || 'Password is required']"
              />
            </div>

            <div class="row justify-between items-center text-caption text-grey-5">
              <q-checkbox v-model="rememberMe" dark label="Remember me" size="sm" color="white" />
              <a href="#" class="text-white text-decoration-none hover-underline"
                >Forgot Password?</a
              >
            </div>

            <q-btn
              unelevated
              color="white"
              text-color="black"
              label="Sign In"
              size="lg"
              no-caps
              class="full-width text-weight-bold q-mt-md"
              style="border-radius: 12px"
              type="submit"
              :loading="loading"
            />
          </q-form>
        </q-card-section>
      </q-card>

      <div class="text-center q-mt-lg text-grey-5">
        Don't have an account?
        <router-link
          to="/register"
          class="text-white text-weight-bold text-decoration-none hover-underline"
          >Get Started</router-link
        >
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref, inject } from 'vue'
import { useRouter } from 'vue-router'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const supabase = inject('supabase')
const router = useRouter()

const email = ref('')
const password = ref('')
const rememberMe = ref(false)
const loading = ref(false)

const handleLogin = async () => {
  loading.value = true
  try {
    const { error } = await supabase.auth.signInWithPassword({
      email: email.value,
      password: password.value,
    })

    if (error) throw error

    $q.notify({
      type: 'positive',
      message: 'Successfully logged in!',
      position: 'top',
    })

    router.push('/')
  } catch (error) {
    $q.notify({
      type: 'negative',
      message: error.message || 'Login failed',
      position: 'top',
    })
  } finally {
    loading.value = false
  }
}
</script>

<style lang="scss" scoped>
.bg-gradient-fade {
  background: linear-gradient(135deg, #000 0%, #111 100%);
}

.input-soft {
  transition: box-shadow 0.3s ease;
  &:focus-within {
    box-shadow: 0 0 0 2px #333;
  }
}

.hover-underline:hover {
  text-decoration: underline !important;
}
</style>
