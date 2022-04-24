<script setup lang="ts">
import { onMounted } from 'vue';
import liff from '@line/liff'
import { IS_PROD, LIFF_ID } from '~/constants'
import Loading from '~/components/Loading.vue'
import HelloWorld from '~/components/HelloWorld.vue'
import Error from '~/components/Error.vue';

let isError = false
let err: any
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
    err = err
    isError = true
    isLoggedIn = false
    userId = null
  }
})
</script>

<template>
  <Error v-if="isError" :err="err" />
  <HelloWorld v-else-if="isLoggedIn" :user-id="`${userId}`" />
  <Loading v-else />
</template>
