<script setup lang="ts">
import TheWelcome from '@/components/TheWelcome.vue'

interface MenuItem {
  label: string;
  link: string;
}

const menu: MenuItem[] = [
  {
    label: 'Departments',
    link: '/about',
  },
  {
    label: 'Staff',
    link: '',
  },
]
</script>

<template>
  <main>
    <div>Company: </div>
  </main>
  <aside>
    <nav>
      <!-- todo: tag="li" doesn't work -->
      <router-link v-for="(item) in menu" :key="item.label" tag="li" :to="item.link">
        {{item.label}}
      </router-link>
    </nav>
  </aside>
</template>
