<template>
  <div class="grid h-full w-full gap-4">
    <div class="flex flex-row items-center justify-between">
      <div>
        <span class="text-white text-xl font-bold">Your Profile</span>
      </div>
    </div>
    <div class="flex flex-row space-x-4">
      <div class="w-[280px] gap-4 border dark:border-gray-800 border-gray-200 rounded-md p-4">
        <StructureMenu :menus="menus" />
      </div>
      <div class="w-full gap-4 border dark:border-gray-800 border-gray-200 rounded-md p-4">
        <NuxtPage />
      </div>
    </div>
  </div>
</template>
<script setup>
definePageMeta({
  layout: "user",
});
</script>
<script>
export default {
  data() {
    return {
      menus: [
        [
          {
            label: "Profile",
            to: "/user/profile",
          },
          {
            label: "Account",
            to: "/user/profile/account",
          },
          {
            label: "Appearance",
            to: "/user/profile/appearance",
          },
          {
            label: "Notifications",
            to: "/user/profile/notifications",
          },
          {
            label: "Display",
            to: "/user/profile/display",
          },
        ],
      ],
    };
  },
};
</script>
