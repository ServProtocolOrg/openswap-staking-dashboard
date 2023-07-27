<script setup lang="ts">
  import OneLogo from "@/assets/one_oswap.png";
</script>

<template>
  <div
    class="flex flex-1 lg:flex-row flex-col justify-between items-center pt-0 lg:pt-20 lg:px-20 max-w-screen-xl mx-auto"
  >
    <div
      class="flex flex-1 flex-col lg:items-start items-center lg:order-1 order-2"
    >
      <span
        class="font-medium text-lg text-oswapGreen-dark text-center lg:text-left"
        >CHOOSE YOUR VALIDATOR & STAKE WISELY</span
      >
      <span
        class="text-3xl lg:text-7xl font-medium capitalize tracking-wider text-center lg:text-left"
        >SERV Staking Portal</span
      >
      <div
        class="flex flex-none w-full justify-center lg:justify-end mt-8"
      >
        <router-link
          :to="'/how-it-works'"
          class="flex items-center space-x-2 p-2 px-1 md:px-3 rounded-lg group focus:outline-none focus:ring-1 focus:ring-black focus:ring-opacity-20"
        >
          <button
            class="p-3 text-lg rounded-lg bg-oswapBlue-light text-white"
          >
            How does it work?
          </button>
        </router-link>
        <router-link
          :to="'/validators'"
          class="flex items-center space-x-2 p-2 px-1 md:px-3 rounded-lg group focus:outline-none focus:ring-1 focus:ring-black focus:ring-opacity-20"
        >
          <button
            class="p-3 text-lg rounded-lg bg-oswapGreen-dark text-white"
          >
            Stake Now!
          </button>
        </router-link>
      </div>
    </div>
    <div
      class="flex flex-1 justify-center items-center lg:order-2 order-1"
    >
      <img class="h-48 w-full lg:h-64" :src="OneLogo" />
    </div>
  </div>
</template>
