<template>
  <router-view />
</template>

<script setup>
import { RouterView } from "vue-router";
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'


const router = useRouter()

onMounted(() => {
router.push('/Weather')
})
</script>

<style scoped>
.footer {
  text-align: center;
  font-size: 10px;
}
</style>