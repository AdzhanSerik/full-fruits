<template>
    <div class="h-[70vh] flex items-center justify-center" v-auto-animate>
        <SignIn :changeStatus="changeStatus" :username="username" :password="password" :toggleSignUp="toggleSignUp"
            v-if="!isSignUp" />
        <SignUp :getUserFromSignUp="getUserFromSignUp" :toggleSignUp="toggleSignUp" v-else />
    </div>
</template>

<script setup>
import SignIn from '../components/SignIn.vue'
import SignUp from '../components/SignUp.vue'

import { ref } from 'vue'

const isSignUp = ref(false)
const username = ref('')
const password = ref('')

defineProps({
    changeStatus: Function
})

function getUserFromSignUp(usernameFromSignUp, passwordFromSignUp) {
    username.value = usernameFromSignUp
    password.value = passwordFromSignUp
}

function toggleSignUp() {
    isSignUp.value = !isSignUp.value
}


</script>

<style lang="scss" scoped></style>