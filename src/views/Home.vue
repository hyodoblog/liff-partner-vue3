<script setup lang="ts">
import { IS_PROD, LIFF_ID } from '~/constants'
import Loading from '~/components/Loading.vue'
import HelloWorld from '~/components/HelloWorld.vue'
import liff from '@line/liff'

let isLoggedIn = false
let userId: string | undefined
if (IS_PROD) {
  liff.init({ liffId: LIFF_ID })
  userId = liff.getContext()?.userId
  isLoggedIn = liff.isLoggedIn()
}
</script>

<template>
  <HelloWorld v-if="isLoggedIn" :user-id="`${userId}`" />
  <Loading v-else />

  {{ LIFF_ID }}
</template>
