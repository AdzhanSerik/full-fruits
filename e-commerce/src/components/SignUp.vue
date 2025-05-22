<template>
    <form @submit.prevent="createUser">
        <div class="flex flex-col justify-center items-center h-full gap-4">
            <h1 class="text-3xl text-[#275B1A] font-bold">Регистрация</h1>
            <input type="text" required class="w-[20vw] outline-none border border-[#327a20] p-2 rounded-[10px]"
                placeholder="Введите никнейм" v-model="username" />
            <input type="email" required class="w-[20vw] outline-none border border-[#327a20] p-2 rounded-[10px]"
                placeholder="Введите почту" v-model="email" />
            <p v-if="errorMessage" class="text-red-600">{{ errorMessage }}</p>
            <input type="password" required class="w-[20vw] outline-none border border-[#327a20] p-2 rounded-[10px]"
                placeholder="Введите пароль" v-model="password" />
            <button type="submit" class="cursor-pointer bg-[#275B1A] text-white py-2 px-10 rounded-[10px]">
                Зарегистрироваться
            </button>
            <p>
                У вас есть аккаунт?
                <span @click="toggleSignUp" class="text-[#275B1A] font-bold cursor-pointer">Войдите</span>
            </p>
            <p v-if="successMessage" class="text-green-600">{{ successMessage }}</p>

        </div>
    </form>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router'; // Если вы хотите перенаправлять пользователя

const props = defineProps({
    toggleSignUp: Function,
    getUserFromSignUp: Function
});

const username = ref('')
const email = ref('')
const password = ref('')

const errorMessage = ref('')
const successMessage = ref('')

async function createUser() {
    try {
        const response = await axios.post('http://localhost:4000/auth/register', {
            username: username.value,
            email: email.value,
            password: password.value
        })

        if (response.status === 201) {
            console.log('Пользователь успешно зарегистрирован')
            props.getUserFromSignUp(username.value, password.value)
            props.toggleSignUp()
        }
    } catch (error) {

        errorMessage.value = 'Пользователь с таким именем уже существует'
        console.log(error)
    }
}

</script>