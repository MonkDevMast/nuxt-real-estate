<template>
  <!-- Footer (Desktop only) -->
  <div
    class="absolute bottom-0 left-0 w-full justify-between items-center px-9 item-center pb-6 pt-5 h-[13%] text-white hidden md:flex"
  >
    <div @click="navigateHome" class="flex items-center gap-3">
      <img
        src="/assets/videos/orb.gif"
        alt=""
        class="h-[85px] md:h-[85px] cursor-pointer"
      />
      
      <p
        class="font-['DM Sans'] text-sm font-normal text-[#CBCBCB] cursor-pointer"
      >
        Get back to Rechitta
      </p>
    </div>
    <Transition name="slide-up" appear>
      <div class="relative right-[30%] bottom-10">
        <MainSection 
          :mic-text="micText"
          :multi="true"
          :is-active="isActive"
          message="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. "
          @toggle="toggleMic"
        />
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import 'vue-tel-input/vue-tel-input.css';
import { Swiper } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/pagination';
import MainSection from '~/components/VoiceInput.vue';

const router = useRouter();

definePageMeta({
  layout: 'blank',
});

useHead({
  title: "Rechitta",
  meta: [
    {
      name: "description",
      content:
        "Discover, explore, and seal deals on premium properties with ease. Your next home or investment is just a click away.",
    },
  ],
});

const isActive = ref(false);

const navigateHome = () => {
  router.push('/')
}

const toggleMic = () => {
  isActive.value = !isActive.value;
  isTransitioning.value = true;
  setTimeout(() => {
    goToProperties();
  }, 500);
};


</script>

<style scoped>

</style>