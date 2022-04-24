<script setup lang="ts">
import { IS_PROD, LIFF_ID } from '~/constants'
import Loading from '~/components/Loading.vue'
import HelloWorld from '~/components/HelloWorld.vue'
import liff from '@line/liff'
import { onMounted } from 'vue';

let isLoggedIn = false
let userId: string | null

onMounted(async () => {
  try {
    if (IS_PROD) {
      await liff.init({ liffId: LIFF_ID })
      userId = liff.getContext()?.userId || null
      isLoggedIn = liff.isLoggedIn()
    }
  } catch (err) {
    console.error(err)
    isLoggedIn = false
    userId = null
  }
})
</script>

<template>
  <HelloWorld v-if="isLoggedIn" :user-id="`${userId}`" />
  <Loading v-else />
</template>
