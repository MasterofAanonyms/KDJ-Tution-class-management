<template>
  <q-page class="bg-black text-white flex flex-center relative-position overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute-full overflow-hidden">
      <!-- Gradient Fade similar to Home -->
      <div class="absolute-full bg-gradient-fade"></div>

      <!-- Decorative blurred circle -->
      <div
        class="absolute-top-left bg-white"
        style="
          width: 300px;
          height: 300px;
          border-radius: 50%;
          opacity: 0.1;
          filter: blur(80px);
          transform: translate(-30%, -30%);
        "
      ></div>

      <div
        class="absolute-bottom-right bg-white"
        style="
          width: 400px;
          height: 400px;
          border-radius: 50%;
          opacity: 0.05;
          filter: blur(100px);
          transform: translate(30%, 30%);
        "
      ></div>
    </div>

    <!-- Register Card -->
    <div class="relative-position z-top" style="width: 100%; max-width: 500px; padding: 20px">
      <div class="text-center q-mb-lg">
        <q-icon name="school" color="white" size="40px" class="q-mb-sm" />
        <div class="text-h4 text-weight-bold">Create Account</div>
        <div class="text-grey-5 q-mt-sm">Join thousands of institutes today</div>
      </div>

      <q-card
        class="bg-grey-10 text-white shadow-24"
        style="border-radius: 24px; border: 1px solid #333"
      >
        <q-card-section class="q-pa-lg q-pa-md-xl">
          <q-form @submit="handleRegister" class="q-gutter-y-md">
            <div class="row q-col-gutter-md">
              <div class="col-12 col-md-6">
                <label
                  class="text-grey-5 q-mb-xs block text-caption text-uppercase text-weight-bold tracking-wider"
                  >First Name</label
                >
                <q-input
                  dark
                  borderless
                  dense
                  v-model="form.firstName"
                  placeholder="John"
                  class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                  :rules="[(val) => !!val || 'Required']"
                />
              </div>
              <div class="col-12 col-md-6">
                <label
                  class="text-grey-5 q-mb-xs block text-caption text-uppercase text-weight-bold tracking-wider"
                  >Last Name</label
                >
                <q-input
                  dark
                  borderless
                  dense
                  v-model="form.lastName"
                  placeholder="Doe"
                  class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                  :rules="[(val) => !!val || 'Required']"
                />
              </div>
            </div>

            <div>
              <label
                class="text-grey-5 q-mb-xs block text-caption text-uppercase text-weight-bold tracking-wider"
                >Email Address</label
              >
              <q-input
                dark
                borderless
                dense
                v-model="form.email"
                placeholder="john@example.com"
                class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                type="email"
                :rules="[(val) => !!val || 'Email is required']"
              />
            </div>

            <div>
              <label
                class="text-grey-5 q-mb-xs block text-caption text-uppercase text-weight-bold tracking-wider"
                >Password</label
              >
              <q-input
                dark
                borderless
                dense
                v-model="form.password"
                placeholder="••••••••"
                class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                type="password"
                :rules="[
                  (val) => !!val || 'Password is required',
                  (val) => val.length >= 6 || 'Min 6 characters',
                ]"
              />
            </div>

            <div>
              <label
                class="text-grey-5 q-mb-xs block text-caption text-uppercase text-weight-bold tracking-wider"
                >Confirm Password</label
              >
              <q-input
                dark
                borderless
                dense
                v-model="form.confirmPassword"
                placeholder="••••••••"
                class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                type="password"
                :rules="[
                  (val) => !!val || 'Confirmation is required',
                  (val) => val === form.password || 'Passwords do not match',
                ]"
              />
            </div>

            <q-btn
              unelevated
              color="white"
              text-color="black"
              label="Create Account"
              size="lg"
              no-caps
              class="full-width text-weight-bold q-mt-lg"
              style="border-radius: 12px"
              type="submit"
              :loading="loading"
            />
          </q-form>
        </q-card-section>
      </q-card>

      <div class="text-center q-mt-lg text-grey-5">
        Already have an account?
        <router-link
          to="/login"
          class="text-white text-weight-bold text-decoration-none hover-underline"
          >Sign In</router-link
        >
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { reactive, ref, inject } from 'vue'
import { useRouter } from 'vue-router'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const supabase = inject('supabase')
const router = useRouter()

const form = reactive({
  firstName: '',
  lastName: '',
  email: '',
  password: '',
  confirmPassword: '',
})

const loading = ref(false)

const handleRegister = async () => {
  loading.value = true
  try {
    const { error } = await supabase.auth.signUp({
      email: form.email,
      password: form.password,
      options: {
        data: {
          first_name: form.firstName,
          last_name: form.lastName,
        },
      },
    })

    if (error) throw error

    $q.notify({
      type: 'positive',
      message: 'Account created successfully!',
      position: 'top',
    })

    router.push('/')
  } catch (error) {
    $q.notify({
      type: 'negative',
      message: error.message || 'Registration failed',
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
