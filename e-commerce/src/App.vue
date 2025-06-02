<template>
  <div class="bg-[#275B1A] px-[100px] py-[50px]">
    <div class="bg-white rounded-[20px] px-[80px]" v-auto-animate>
      <Header :authStatus="authStatus" :authorized="authorized" :toggleCart="toggleCart" />

      <router-view :changeStatus="changeStatus" :authorized="authorized" :isOpenCart="isOpenCart"
        :toggleCart="toggleCart">
      </router-view>
    </div>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";

import { ref, watch } from "vue"
const isOpenCart = ref(false)
const authorized = ref('')
const authStatus = ref(true)

watch(authStatus, () => {
  console.log(authStatus.value)
})

function changeStatus() {
  authStatus.value = false
}

function toggleCart() {
  isOpenCart.value = !isOpenCart.value
}
</script>
