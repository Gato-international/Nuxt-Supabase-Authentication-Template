<template>
  <div
    class="bg-gradient-to-b from-gray-900 to-primary-400/0 h-full xl:p-12 duration-150 transition-all"
  >
    <div
      class="fixed inset-0 flex lg:overflow-hidden antialiased font-sans text-gray-700 dark:text-gray-200 select-none bg-gray-950 xl:mt-12 xl:mx-4 rounded-t-lg"
    >
      <StructureSidebar />
      <div class="flex flex-col w-full overflow-y-scroll">
        <div class="mt-10 mx-10 static top-0">
          <StructureBreadCrumbs />
        </div>
        <div class="m-10">
          <slot />
        </div>       
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: true,
    };
  },
};
</script>
<style>
/* Webkit Scrollbar */
::-webkit-scrollbar {
  width: 8px; /* Width of the scrollbar */
}

::-webkit-scrollbar-track {
  background: #1e1e1e; /* Dark background for the track */
}

::-webkit-scrollbar-thumb {
  background: #444; /* Dark color for the thumb */
  border-radius: 4px; /* Rounded corners for the thumb */
}

::-webkit-scrollbar-thumb:hover {
  background: #555; /* Slightly lighter color when hovered */
}

</style>

