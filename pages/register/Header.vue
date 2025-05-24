<template>
  <!-- Header -->
  <div class="absolute z-50 top-0 left-0 w-full flex justify-between items-center pt-5 sm:pt-4 pb-5 sm:pb-7 px-5 sm:px-9 lg:h-[15vh] h-[10%]  sm:bg-transparent">
    <img
      src="/assets/images/richitta-logo.svg"
      alt="Rechitta Logo"
      class="h-3 sm:h-5 cursor-pointer"
      @click="navigateHome"
    />
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { usePageLayoutStore } from '~/stores/pagelayoutStore';

const store = usePageLayoutStore();

const router = useRouter();

const navigateHome = () => {
  store.setLayout('main');
  // router.push('/')
}

</script>

<style scoped>

</style>