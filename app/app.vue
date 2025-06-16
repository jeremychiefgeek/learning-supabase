<script setup lang="ts">
import { createClient } from '@supabase/supabase-js';
const config = useRuntimeConfig()
const supabase = createClient(config.public.supabaseUrl, config.public.supabaseAnonKey);
onMounted(() => {
  supabase.storage.listBuckets().then((result) => {
    console.log("Bucket list", result);
  })
});
</script>
<template>
  <UApp>
    <NuxtPage />
  </UApp>
</template>
