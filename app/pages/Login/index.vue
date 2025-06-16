<script setup lang="ts">
  const route = useRoute();
  console.log(route.query);
  const wantsMagicLink = ref(route.query.magicLink === 'yes');
</script>
<template>
  <div class="flex flex-col items-center justify-center gap-4 h-screen">
    <LoginForm :shouldShowMagicLink="wantsMagicLink"/>
  </div>
</template>
