<template>
  <q-page class="q-pa-lg">
    <div class="row q-col-gutter-lg">
      <!-- Welcome Section -->
      <div class="col-12">
        <div class="text-h4 text-weight-bold q-mb-sm">Dashboard</div>
        <div class="text-grey-5">Welcome back to your institute management overview.</div>
      </div>

      <!-- Stats Cards -->
      <div class="col-12 col-sm-6 col-md-3" v-for="stat in stats" :key="stat.title">
        <q-card class="bg-grey-10 text-white" style="border-radius: 16px; border: 1px solid #333">
          <q-card-section>
            <div class="row items-center justify-between q-mb-md">
              <div class="text-grey-5">{{ stat.title }}</div>
              <q-icon :name="stat.icon" size="24px" :color="stat.color" />
            </div>
            <div class="text-h4 text-weight-bold">{{ stat.value }}</div>
            <div class="text-caption" :class="stat.trend > 0 ? 'text-green' : 'text-red'">
              <q-icon :name="stat.trend > 0 ? 'trending_up' : 'trending_down'" />
              {{ Math.abs(stat.trend) }}% vs last month
            </div>
          </q-card-section>
        </q-card>
      </div>

      <!-- Recent Activity or Other Content -->
      <div class="col-12 col-md-8">
        <q-card
          class="bg-grey-10 text-white full-height"
          style="border-radius: 16px; border: 1px solid #333"
        >
          <q-card-section>
            <div class="text-h6 text-weight-bold q-mb-md">Recent Activity</div>
            <div class="text-grey-5 text-center q-py-xl">No recent activity to show.</div>
          </q-card-section>
        </q-card>
      </div>

      <div class="col-12 col-md-4">
        <q-card
          class="bg-grey-10 text-white full-height"
          style="border-radius: 16px; border: 1px solid #333"
        >
          <q-card-section>
            <div class="text-h6 text-weight-bold q-mb-md">Quick Actions</div>
            <div class="q-gutter-y-sm">
              <q-btn
                outline
                color="white"
                label="Add Student"
                class="full-width"
                icon="person_add"
                no-caps
              />
              <q-btn
                outline
                color="white"
                label="Create Class"
                class="full-width"
                icon="class"
                no-caps
              />
              <q-btn
                outline
                color="white"
                label="Record Payment"
                class="full-width"
                icon="payments"
                no-caps
              />
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script setup>
const stats = [
  { title: 'Total Students', value: '1,245', icon: 'people', color: 'blue', trend: 12 },
  { title: 'Active Classes', value: '34', icon: 'class', color: 'orange', trend: 5 },
  { title: 'Revenue', value: '$12.4k', icon: 'payments', color: 'green', trend: 8 },
  { title: 'New Enrolls', value: '45', icon: 'person_add', color: 'purple', trend: -2 },
]
</script>
