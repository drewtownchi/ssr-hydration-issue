<template>
  <h1>Welcome</h1>
  <Nav :navigation="navigation" />
</template>

<script lang="ts" setup>
import Nav from './Nav.vue'

const navigation = [
  { name: 'Home', href: '/' },
  { name: 'Search', href: '#' },
  {
    name: 'Calculators',
    children: [
      { name: 'Blood & plasma volume', href: '#' },
    ],
  }
]
</script>
