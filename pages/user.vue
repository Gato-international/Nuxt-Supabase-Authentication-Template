<template>
    <NuxtPage />
</template>
<script setup>
definePageMeta({
  layout: "user",
});
defineNuxtRouteMiddleware((to, from) => {
  if (to.path === "/user") {
    return navigateTo("/user/dashboard");
  }
})
</script>