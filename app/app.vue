<script setup lang="ts">
const supabase = useSupabaseClient()
onMounted(() => {
  supabase.storage.listBuckets().then((result: any) => {
    console.log("Bucket list", result);
  })
});
</script>
<template>
  <UApp>
    <NuxtPage />
  </UApp>
</template>
