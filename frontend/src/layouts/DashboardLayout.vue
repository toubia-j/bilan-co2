<script setup>
import SideBar from "../components/dashboard/sidebar/SideBar.vue";
</script>

<template>
  <div class="grid h-screen grid-cols-12 grid-rows-24 overflow-hidden">
    <div class="col-start-4 col-end-[-1] row-start-1 row-end-2 border-b pl-1">
      <h2 class="">pages / {{ currentRouteName }}</h2>
    </div>
    <div class="col-start-1 col-end-4 row-start-1 row-end-[-1] bg-[#03C988]">
      <SideBar class="h-full" />
    </div>
    <router-view
      class="col-start-4 col-end-[-1] row-start-2 row-end-[-1] bg-slate-50"
    ></router-view>
  </div>
</template>

<script>
export default {
  computed: {
    currentRouteName() {
      return this.$route.name;
    },
  },
};
</script>
