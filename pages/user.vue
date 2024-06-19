<template>
    <NuxtPage />
</template>
<script setup>
definePageMeta({
  layout: "user",
});
defineNuxtRouteMiddleware((to, from) => {
  console.log("to", to);  
  if (to.path === "/user") {
    return navigateTo("/user/dashboard");
  }
})
</script>