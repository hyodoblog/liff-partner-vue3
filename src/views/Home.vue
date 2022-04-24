<script setup lang="ts">
import liff from '@line/liff'
import { IS_PROD, LIFF_ID } from '~/constants'
import Loading from '~/components/Loading.vue'
import HelloWorld from '~/components/HelloWorld.vue'

let isLoggedIn = false
let userId: string | null

if (IS_PROD) {
  liff.init({ liffId: LIFF_ID })
  liff.ready.then(() => {
    console.info(liff.isInClient)
    console.info(liff.isInClient())
    console.info(liff.isLoggedIn)
    console.info(liff.isLoggedIn())
    console.info(liff)
    userId = liff.getContext()?.userId || null
    isLoggedIn = liff.isLoggedIn()
  })
} else {
  isLoggedIn = true
  userId = 'test'
}
</script>

<template>
  <HelloWorld v-if="isLoggedIn" :user-id="`${userId}`" />
  <Loading v-else />
</template>
