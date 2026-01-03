<template>
  <q-page class="bg-black text-white">
    <!-- Loading Overlay -->
    <div v-if="isLoading" class="loading-overlay">
      <div class="column items-center">
        <div class="loading-spinner q-mb-md"></div>
        <div class="text-white text-uppercase tracking-widest text-weight-bold">KDJ Tuition</div>
      </div>
    </div>

    <!-- Hero Section -->
    <section class="q-py-lg q-py-md-xl q-px-md relative-position overflow-hidden">
      <!-- Mobile Hero Background -->
      <div class="absolute-full lt-md overflow-hidden">
        <q-img
          :src="heroImage"
          class="full-width full-height"
          fit="cover"
          style="opacity: 0.4; filter: blur(3px) brightness(0.6); transform: scale(1.1)"
        />
        <div class="absolute-full bg-gradient-fade"></div>
      </div>

      <div
        class="row items-center justify-between q-col-gutter-xl container-limit q-mx-auto relative-position hero-grid"
        style="min-height: 80vh; z-index: 1"
      >
        <div class="col-12 col-md-6 text-center text-md-left reveal">
          <q-badge
            color="white"
            text-color="black"
            class="q-py-sm q-px-md text-weight-bold q-mb-md"
            label="100% FREE FOREVER"
          />
          <div class="text-h3 text-md-h1 text-weight-bolder leading-tight q-mb-md">
            Manage your <span class="text-grey-5">Tuition Class</span> completely free.
          </div>
          <p class="text-h6 text-md-h5 text-grey-5 q-mb-lg" style="line-height: 1.6">
            The all-in-one platform designed to streamline student management, payments, and
            attendance. No credit cards, no hidden fees.
          </p>
          <div class="row q-gutter-md justify-center justify-md-start">
            <q-btn
              unelevated
              color="white"
              text-color="black"
              size="lg"
              label="Get Started for Free"
              no-caps
              class="text-weight-bold q-px-xl"
              style="border-radius: 12px"
              to="/register"
            />
            <q-btn
              outline
              color="grey-5"
              size="lg"
              label="Watch Demo"
              no-caps
              class="text-weight-bold q-px-xl"
              style="border-radius: 12px"
            />
          </div>

          <div class="row q-mt-xl justify-center justify-md-start" style="gap: 24px">
            <div>
              <div class="text-h4 text-weight-bold">500+</div>
              <div class="text-caption text-grey-6">Institutes</div>
            </div>
            <div>
              <div class="text-h4 text-weight-bold">10k+</div>
              <div class="text-caption text-grey-6">Students</div>
            </div>
            <div>
              <div class="text-h4 text-weight-bold">99.9%</div>
              <div class="text-caption text-grey-6">Uptime</div>
            </div>
          </div>
        </div>

        <div
          class="col-12 col-md-6 relative-position q-mt-xl q-mt-md-none gt-sm reveal"
          style="transition-delay: 0.2s"
        >
          <q-img
            :src="heroImage"
            class="rounded-borders shadow-24"
            style="border-radius: 24px; filter: grayscale(100%); opacity: 0.9"
          />
          <!-- Decorative blurred circle behind -->
          <div
            class="absolute-center bg-white"
            style="
              width: 300px;
              height: 300px;
              border-radius: 50%;
              opacity: 0.1;
              filter: blur(80px);
              z-index: -1;
            "
          ></div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="q-py-xl bg-dark-page">
      <div class="container-limit q-mx-auto q-px-md">
        <div class="text-center q-mb-xl reveal">
          <div class="text-overline text-grey-5 q-mb-sm">KEY FEATURES</div>
          <h2 class="text-h4 text-md-h3 text-weight-bold q-my-none">Everything you need to grow</h2>
        </div>

        <div class="row q-col-gutter-lg">
          <div
            v-for="(feature, index) in features"
            :key="index"
            class="col-12 col-sm-6 col-md-4 reveal"
            :style="{ transitionDelay: `${index * 0.1}s` }"
          >
            <q-card
              class="bg-grey-10 text-white no-shadow cursor-pointer hover-card"
              style="border-radius: 16px; border: 1px solid #333"
            >
              <q-card-section class="q-pa-lg">
                <div class="q-mb-md bg-black inline-block q-pa-md rounded-borders">
                  <q-icon :name="feature.icon" size="32px" color="white" />
                </div>
                <div class="text-h5 text-weight-bold q-mb-sm">{{ feature.title }}</div>
                <div class="text-grey-5">{{ feature.desc }}</div>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- Dashboard Showcase -->
    <section class="q-py-xl q-px-md">
      <div class="container-limit q-mx-auto">
        <div class="text-center q-mb-xl reveal">
          <h2 class="text-h4 text-md-h3 text-weight-bold q-mb-md">Powerful Analytics Dashboard</h2>
          <p class="text-h6 text-grey-5" style="max-width: 700px; margin: 0 auto">
            Get a bird's-eye view of your entire institute. Our dashboard aggregates data from all
            modules to give you actionable insights in real-time.
          </p>
        </div>

        <div class="row items-center q-col-gutter-xl">
          <!-- Dashboard Image Side -->
          <div class="col-12 col-md-8 q-mb-xl q-mb-md-none reveal">
            <div class="relative-position">
              <q-img
                :src="dashboardImage"
                class="rounded-borders shadow-24"
                style="border-radius: 20px; border: 1px solid #333"
              />
              <!-- Glow Effect -->
              <div
                class="absolute-center bg-white full-width full-height"
                style="opacity: 0.05; filter: blur(60px); z-index: -1"
              ></div>
            </div>
          </div>

          <!-- Description Side -->
          <div class="col-12 col-md-4 reveal" style="transition-delay: 0.2s">
            <div class="q-gutter-y-xl">
              <div>
                <div class="row items-center q-gutter-x-sm q-mb-sm">
                  <q-icon name="payments" size="24px" color="white" />
                  <div class="text-h6 text-weight-bold">Financial Overview</div>
                </div>
                <p class="text-grey-5">
                  Track daily income, pending fees, and monthly revenue trends instantly. Never miss
                  a payment again.
                </p>
              </div>

              <div>
                <div class="row items-center q-gutter-x-sm q-mb-sm">
                  <q-icon name="trending_up" size="24px" color="white" />
                  <div class="text-h6 text-weight-bold">Student Growth</div>
                </div>
                <p class="text-grey-5">
                  Monitor new enrollments and drop-out rates. Visualize your institute's growth
                  trajectory with clear graphs.
                </p>
              </div>

              <div>
                <div class="row items-center q-gutter-x-sm q-mb-sm">
                  <q-icon name="fact_check" size="24px" color="white" />
                  <div class="text-h6 text-weight-bold">Attendance Stats</div>
                </div>
                <p class="text-grey-5">
                  See live attendance numbers for ongoing classes. Identify irregular students at a
                  glance.
                </p>
              </div>

              <q-btn
                flat
                no-caps
                label="View full features"
                icon-right="arrow_forward"
                color="grey-4"
              />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Courses Section -->
    <section class="q-py-xl q-px-md">
      <div class="container-limit q-mx-auto">
        <div class="text-center q-mb-xl reveal">
          <h2 class="text-h4 text-md-h3 text-weight-bold q-my-none">Explore Our Classes</h2>
          <p class="text-grey-5 text-h6 q-mt-sm">Join the best tuition classes in town.</p>
        </div>

        <div class="row q-col-gutter-lg">
          <div
            v-for="(course, i) in courses"
            :key="i"
            class="col-12 col-md-4 reveal"
            :style="{ transitionDelay: `${i * 0.15}s` }"
          >
            <q-card class="bg-dark-page text-white border-grey col-grow flex column" flat>
              <q-img :src="course.img" :ratio="16 / 9" />
              <q-card-section>
                <div class="text-caption text-grey-5 uppercase q-mb-xs">{{ course.subject }}</div>
                <div class="text-h5 text-weight-bold q-mb-sm">{{ course.title }}</div>
                <div class="row items-center q-gutter-x-sm text-grey-4 text-subtitle2">
                  <q-icon name="schedule" />
                  <span>{{ course.time }}</span>
                </div>
              </q-card-section>
              <q-space />
              <q-card-actions align="right">
                <q-btn flat no-caps color="white" label="View Details" icon-right="arrow_forward" />
              </q-card-actions>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Us Section -->
    <section
      class="q-py-xl q-px-md relative-position overflow-hidden"
      style="background: linear-gradient(to bottom, #000000, #0a0a0a)"
    >
      <div class="container-limit q-mx-auto relative-position q-py-lg">
        <div class="row q-col-gutter-xl items-stretch">
          <div
            class="col-12 col-md-5 flex column justify-center q-mb-xl q-mb-md-none text-center text-md-left reveal"
          >
            <div>
              <div class="row items-center justify-center justify-md-start q-gutter-x-sm q-mb-md">
                <q-icon name="support_agent" color="white" size="24px" />
                <span class="text-subtitle1 text-white">24/7 Support</span>
              </div>
              <h2 class="text-h3 text-md-h2 text-weight-bolder leading-tight q-mb-md">
                Let’s start a conversation
              </h2>
              <p class="text-h6 text-grey-6 q-mb-xl">
                Need a custom plan or have a question? Our team is ready to help you transform your
                institute.
              </p>

              <div class="q-gutter-y-lg">
                <a
                  href="mailto:hello@kdj-tuition.com"
                  class="row items-center justify-center justify-md-start q-gutter-x-md text-decoration-none hover-opacity"
                  style="text-decoration: none"
                >
                  <div class="bg-grey-10 q-pa-md rounded-borders">
                    <q-icon name="email" color="white" size="24px" />
                  </div>
                  <div>
                    <div class="text-caption text-grey-5 uppercase text-weight-bold">Email Us</div>
                    <div class="text-h6 text-white leading-tight">hello@kdj-tuition.com</div>
                  </div>
                </a>

                <div class="row items-center justify-center justify-md-start q-gutter-x-md">
                  <div class="bg-grey-10 q-pa-md rounded-borders">
                    <q-icon name="phone" color="white" size="24px" />
                  </div>
                  <div>
                    <div class="text-caption text-grey-5 uppercase text-weight-bold">Call Us</div>
                    <div class="text-h6 text-white leading-tight">+94 77 123 4567</div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="col-12 col-md-7 reveal" style="transition-delay: 0.2s">
            <div
              class="bg-grey-10 q-pa-lg q-pa-md-xl rounded-borders shadow-10"
              style="border-radius: 32px"
            >
              <q-form class="q-gutter-y-lg">
                <div>
                  <label
                    class="text-grey-5 q-mb-sm block text-caption text-uppercase text-weight-bold tracking-wider"
                    >Full Name</label
                  >
                  <q-input
                    dark
                    borderless
                    dense
                    v-model="contactForm.name"
                    placeholder="John Doe"
                    class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                  />
                </div>

                <div>
                  <label
                    class="text-grey-5 q-mb-sm block text-caption text-uppercase text-weight-bold tracking-wider"
                    >Email Address</label
                  >
                  <q-input
                    dark
                    borderless
                    dense
                    v-model="contactForm.email"
                    placeholder="john@example.com"
                    class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                  />
                </div>

                <div>
                  <label
                    class="text-grey-5 q-mb-sm block text-caption text-uppercase text-weight-bold tracking-wider"
                    >Message</label
                  >
                  <q-input
                    dark
                    borderless
                    dense
                    v-model="contactForm.message"
                    type="textarea"
                    rows="4"
                    placeholder="How can we help you?"
                    class="bg-black q-px-md q-py-sm rounded-borders input-soft"
                  />
                </div>

                <div class="q-pt-md">
                  <q-btn
                    unelevated
                    color="white"
                    text-color="black"
                    label="Send Message"
                    size="lg"
                    no-caps
                    class="full-width text-weight-bold"
                    style="border-radius: 12px"
                  />
                </div>
              </q-form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- New CTA Section -->
    <section class="q-py-xl q-px-md reveal">
      <div class="container-limit q-mx-auto q-my-xl">
        <div class="bg-grey-10 relative-position overflow-hidden" style="border-radius: 30px">
          <div
            class="absolute-full"
            style="background: linear-gradient(45deg, #111 0%, #333 100%); opacity: 0.5"
          ></div>
          <div class="row items-center relative-position q-pa-xl">
            <div class="col-12 col-md-8 text-center text-md-left q-mb-lg q-mb-md-none">
              <h2 class="text-h4 text-md-h3 text-weight-bolder q-mb-md">
                Ready to Transform Your Institute?
              </h2>
              <p class="text-h6 text-grey-4">
                Join 500+ institutes managing their classes smarter, faster, and better.
              </p>
            </div>
            <div class="col-12 col-md-4 text-center text-md-right">
              <q-btn
                unelevated
                color="white"
                text-color="black"
                size="lg"
                label="Get Started Now"
                no-caps
                class="text-weight-bold q-px-xl shadow-10"
                style="border-radius: 12px"
                to="/register"
              />
            </div>
          </div>
        </div>
      </div>
    </section>
  </q-page>
</template>

<script setup>
import { reactive, ref, onMounted, onUnmounted } from 'vue'
import heroImage from 'assets/hero-image.png'
import dashboardImage from 'assets/dashboard-mockup.png'
import physicsImg from 'assets/class-physics.png'
import mathImg from 'assets/class-math.png'
import codingImg from 'assets/class-coding.png'

const isLoading = ref(true)
const contactForm = reactive({
  name: '',
  email: '',
  message: '',
})

const courses = [
  {
    title: 'Advanced Level Physics',
    subject: 'Physics',
    time: 'Mon & Wed, 3:30 PM',
    img: physicsImg,
  },
  {
    title: 'Combined Mathematics',
    subject: 'Mathematics',
    time: 'Tue & Thu, 4:00 PM',
    img: mathImg,
  },
  {
    title: 'Introduction to Programming',
    subject: 'Computer Science',
    time: 'Sat, 9:00 AM',
    img: codingImg,
  },
]

const features = [
  {
    icon: 'people',
    title: 'Student Management',
    desc: 'Effortlessly manage student profiles, enrollments, and history in one place.',
  },
  {
    icon: 'payments',
    title: 'Smart Payments',
    desc: 'Track fee payments, generate receipts, and get financial reports instantly.',
  },
  {
    icon: 'qr_code_scanner',
    title: 'Automated Attendance',
    desc: 'QR code based attendance system to keep track of every student entry.',
  },
  {
    icon: 'insights',
    title: 'Advanced Analytics',
    desc: 'Gain insights into your institutes performance with detailed graphs.',
  },
  {
    icon: 'notifications',
    title: 'Instant Alerts',
    desc: 'Send SMS and payment reminders to parents automatically.',
  },
  {
    icon: 'lock',
    title: 'Secure & Reliable',
    desc: 'Your data is encrypted and backed up daily for maximum security.',
  },
]

// Scroll Animation Observer
let observer
onMounted(() => {
  // Simulate initial load
  setTimeout(() => {
    isLoading.value = false

    // Initialize observer after loading is done and DOM is ready
    setTimeout(() => {
      observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              entry.target.classList.add('reveal-active')
              observer.unobserve(entry.target) // Only animate once
            }
          })
        },
        {
          threshold: 0.1,
          rootMargin: '50px',
        },
      )

      const elements = document.querySelectorAll('.reveal')
      elements.forEach((el) => observer.observe(el))
    }, 100)
  }, 1500)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<style lang="scss" scoped>
.container-limit {
  max-width: 1200px;
}
.leading-tight {
  line-height: 1.1;
}
.hover-card {
  transition:
    transform 0.3s ease,
    background-color 0.3s ease;
  &:hover {
    transform: translateY(-5px);
    background-color: #262626 !important; // Slightly lighter grey
  }
}
.bg-dark-page {
  background-color: #0d0d0d;
}
.border-grey {
  border: 1px solid #333;
}
.tracking-wider {
  letter-spacing: 0.05em;
}
.input-soft {
  transition: box-shadow 0.3s ease;
  &:focus-within {
    box-shadow: 0 0 0 2px #333;
  }
}
.hover-opacity {
  transition: opacity 0.3s;
  &:hover {
    opacity: 0.7;
  }
}

// Responsive typography
@media (min-width: 1024px) {
  .text-md-h1 {
    font-size: 6rem;
    line-height: 1.1;
  }
  .text-md-h2 {
    font-size: 3.75rem;
    line-height: 1.2;
  }
  .text-md-h3 {
    font-size: 3rem;
  }
  .text-md-h5 {
    font-size: 1.5rem;
  }
  .text-md-left {
    text-align: left;
  }
  .justify-md-start {
    justify-content: flex-start;
  }
  .q-pa-md-xl {
    padding: 48px;
  }
  .q-mt-md-none {
    margin-top: 0;
  }
  .q-mb-md-none {
    margin-bottom: 0;
  }
}
@media (max-width: 1023px) {
  .text-md-right {
    text-align: center;
  }
  /* Remove gutter shift on mobile for hero */
  .hero-grid {
    margin-left: 0 !important;
  }
  .hero-grid > div {
    padding-left: 0 !important;
  }
}

.bg-gradient-fade {
  background: linear-gradient(to top, #000 0%, rgba(0, 0, 0, 0.6) 100%);
}

/* Loading Overlay */
.loading-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #000;
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
  transition:
    opacity 0.5s ease,
    visibility 0.5s;
}

.loading-spinner {
  width: 50px;
  height: 50px;
  border: 4px solid #333;
  border-top: 4px solid #fff;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

/* Scroll Animations */
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.5, 0, 0, 1);
}

.reveal-active {
  opacity: 1;
  transform: translateY(0);
}
</style>
