<template>
    <form @submit.prevent="login">
        <div class="flex flex-col justify-center items-center h-full gap-4">
            <h1 class="text-3xl text-[#275B1A] font-bold">Авторизация</h1>
            <input type="text" class="w-[20vw] outline-none border border-[#327a20] p-2 rounded-[10px]"
                placeholder="Введите почту или никнейм" v-model="usernameUser" />
            <input type="text" class="w-[20vw] outline-none border border-[#327a20] p-2 rounded-[10px]"
                placeholder="Введите пароль" v-model="passwordUser" />
            <p v-if="errorMessage" class="text-red-600">{{ errorMessage }}</p>
            <button class="cursor-pointer bg-[#275B1A] text-white py-2 px-10 rounded-[10px]">Войти</button>
            <p>У вас нет аккаунта? <span @click="toggleSignUp"
                    class="text-[#275B1A] font-bold cursor-pointer">Зарегистрируйтесь</span></p>
        </div>
    </form>
</template>

<script setup>
const props = defineProps({
    toggleSignUp: Function,
    username: String,
    password: String,
    changeStatus: Function
})

import { ref } from 'vue'
import axios from 'axios';
import router from '../router';

const usernameUser = ref('')
const passwordUser = ref('')
const errorMessage = ref('')

async function login() {
    try {
        const response = await axios.post('http://localhost:4000/auth/login', {
            identifier: usernameUser.value,
            password: passwordUser.value
        })

        if (response.status === 200) {
            props.changeStatus(true)
            router.push('/')
        }
    } catch (error) {
        errorMessage.value = 'Неверные учетные данные'
        console.log(error)
    }
}

</script>
