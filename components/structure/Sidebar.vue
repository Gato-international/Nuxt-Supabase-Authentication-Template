<template>
  <div class="hidden lg:flex lg:flex-shrink-0">
    <div
      class="flex flex-col flex-shrink-0 w-56 xl:w-64 min-w-[14rem] max-w-xs border-r dark:border-gray-700 relative"
      style="width: 224px"
    >
      <div class="flex flex-col flex-1 min-h-0 relative">
        <div class="flex items-center justify-stretch px-4 h-14">
          <StructureLogo />
          <UtilitiesColorModeButton />
        </div>
        <div class="relative flex flex-col flex-1 overflow-hidden my-4">
          <div class="lg:mt-0 px-2" v-for="menu of menus">
            <UVerticalNavigation :links="menu" />
            <hr class="mx-4 my-4 border-t dark:border-gray-700" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      actionsOpen: true,
      menus: [
        [
          {
            label: "Dashboard",
            icon: "i-heroicons-home",
            to: "/",
          },
          {
            label: "Actions",
            icon: "i-heroicons-cog",
            to: "/actions",
          },
          {
            label: "Settings",
            icon: "i-heroicons-cog",
            to: "/settings",
          },
          {
            label: "Profile",
            icon: "i-heroicons-user",
            to: "/profile",
          },
        ],
        [
          {
            label: "Settings",
            icon: "i-heroicons-cog",
            to: "/settings",
          },
          {
            label: "Profile",
            icon: "i-heroicons-user",
            to: "/profile",
          },
        ]
      ],
    };
  },
};
</script>
<style></style>
