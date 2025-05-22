<template>
  <div class="bg-[#275B1A] px-[100px] py-[50px]">
    <div class="bg-white rounded-[20px] px-[80px]" v-auto-animate>
      <Header :authorized="authorized" :toggleCart="toggleCart" />

      <router-view :authorized="authorized" :isOpenCart="isOpenCart" :toggleCart="toggleCart">
      </router-view>
    </div>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";

import { ref } from "vue"
const isOpenCart = ref(false)
const authorized = ref('')

function toggleCart() {
  isOpenCart.value = !isOpenCart.value
}
</script>
