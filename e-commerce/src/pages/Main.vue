<template>
    <div>
        <Slider />
        <Search :searchProducts="searchProducts" />
        <AllProducts :fruits="fruits" />
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import Slider from '../components/Slider.vue'
import AllProducts from '../components/AllProducts.vue'
import Search from '../components/Search.vue'


const fruits = ref([])
const compareFruits = ref([])

const props = defineProps({
    changeStatus: Function
})

async function getAllProducts() {
    try {
        const response = await axios.get("http://localhost:4000/api/fruits")
        return response.data
    } catch (error) {
        console.log(error.response.status)
        props.changeStatus()
        return []
    }
}

// async function auth() {
//     try {
//         const response = await axios.post("http://localhost:4000/auth/login", {

//             identifier: "Adzhan",
//             password: "qwerty"

//         })
//         console.log(response)

//     } catch (error) {

//     }
// }

async function logout() {
    try {
        const response = await axios.post("http://localhost:4000/auth/logout")
    } catch (error) {
        console.log(error)
    }
}

async function searchProducts(event) {

    fruits.value = compareFruits.value.filter((fruit) => {
        return fruit.title.toLowerCase().includes(event.target.value.toLowerCase())
    })
    console.log(fruits.value)
}

onMounted(async () => {
    // await auth()
    // logout()
    fruits.value = await getAllProducts()
    console.log('aaaa: ', fruits.value)
    compareFruits.value = fruits.value
    console.log(fruits.value)
})

</script>

<style lang="scss" scoped></style>