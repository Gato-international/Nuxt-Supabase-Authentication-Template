<template>
  <UBreadcrumb :links="crumbs">
    <template #icon="{ link, index, isActive }">
      <icon :name="link.icon" class="w-4 h-4" />
    </template>
  </UBreadcrumb>
</template>
<script>
export default {
  computed: {
    crumbs() {
      const route = this.$route;
      const crumbs = route.path.split("/").filter((crumb) => crumb !== "");
      return crumbs.map((crumb, index) => {
        return {
          label: crumb,
          to: '/' + crumbs.slice(0, index + 1).join("/"),
          icon: "ri:dashboard-fill",
        };
      });
    },
  },
};
</script>
