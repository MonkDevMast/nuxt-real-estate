<template>
  <!-- Mobile Layout (form first, then card) -->

  <div class="w-full mt-32 md:mt-0 px-5 pb-20 md:hidden flex flex-col gap-6">
    <!-- Form -->
    <div 
      class="bg-[#111111] rounded-xl p-6 w-full"
      :style="{ boxShadow: '0px 10px 60px 15px rgba(255, 255, 255, 0.4)' }"
    >
      <h2 class="text-xl font-semibold mb-2 font-machina-plain">Register Your Interest</h2>
      <p class="text-[#999999] mb-6 text-sm">Let us know what you're looking for</p>
      
      <form @submit.prevent="submitForm">
        <div class="mb-4">
          <label class="block mb-1.5 text-sm text-[#cccccc]">Full Name <span class="text-[#50B9E0]">*</span></label>
          <input 
            type="text" 
            v-model="formData.fullName" 
            placeholder="Timothy Ricks" 
            class="w-full px-3 py-2 rounded-md bg-[#1a1a1a] border border-[#333333] text-[#50B9E0] text-sm placeholder-[#666666] focus:border-[#50B9E0] focus:outline-none"
            required
          />
        </div>
        
        <div class="mb-4">
          <label class="block mb-1.5 text-sm text-[#cccccc]">Email <span class="text-[#50B9E0]">*</span></label>
          <input 
            type="email" 
            v-model="formData.email" 
            placeholder="Enter your Email" 
            class="w-full px-3 py-2 rounded-md bg-[#1a1a1a] border border-[#333333] text-[#50B9E0] text-sm placeholder-[#666666] focus:border-[#50B9E0] focus:outline-none"
            required
          />
        </div>
        
        <div class="mb-4">
          <label class="block mb-1.5 text-sm text-[#cccccc]">Contact Number <span class="text-[#50B9E0]">*</span></label>
          <vue-tel-input
            v-model="formData.contactNumber"
            :inputOptions="{
              placeholder: 'Enter your Number',
              classes: 'w-full px-3 py-2 rounded-md bg-[#1a1a1a] border border-[#333333] text-[#50B9E0] text-sm placeholder-[#666666] focus:border-[#50B9E0] focus:outline-none'
            }"
            :dropdownOptions="{
              showDialCodeInSelection: true,
              showFlags: true,
              showDialCodeInList: true,
              dropdownClass: 'bg-[#1a1a1a] border border-[#333333] text-white'
            }"
            mode="international"
            required
          />
        </div>
        
        <div class="mb-4">
          <label class="block mb-1.5 text-sm text-[#cccccc]">Unit Number <span class="text-[#50B9E0]">*</span></label>
          <input 
            type="text" 
            v-model="formData.unitNumber" 
            placeholder="1702 (Select / Search From Available Units)" 
            class="w-full px-3 py-2 rounded-md bg-[#1a1a1a] border border-[#333333] text-[#50B9E0] text-sm placeholder-[#666666] focus:border-[#50B9E0] focus:outline-none"
            required
          />
        </div>
        
        <div class="mb-4">
          <label class="block mb-1.5 text-sm text-[#cccccc]">Broker Name <span class="text-[#50B9E0]">*</span></label>
          <div class="relative">
            <input 
              type="text" 
              v-model="formData.brokerName" 
              placeholder="Broker Name (auto select)" 
              class="w-full px-3 py-2 rounded-md bg-[#1a1a1a] border border-[#333333] text-[#50B9E0] text-sm placeholder-[#666666] focus:border-[#50B9E0] focus:outline-none"
              readonly
            />
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-chevron-down absolute right-3 top-1/2 -translate-y-1/2 pointer-events-none"><path d="m6 9 6 6 6-6"></path></svg>
          </div>
        </div>
        
        <div class="mb-6">
          <label class="block mb-1.5 text-sm text-[#cccccc]">Broker Agency <span class="text-[#50B9E0]">*</span></label>
          <div class="relative">
            <input 
              type="text" 
              v-model="formData.brokerAgency" 
              placeholder="Broker Agency (auto select)" 
              class="w-full px-3 py-2 rounded-md bg-[#1a1a1a] border border-[#333333] text-[#50B9E0] text-sm placeholder-[#666666] focus:border-[#50B9E0] focus:outline-none"
              readonly
            />
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-chevron-down absolute right-3 top-1/2 -translate-y-1/2 pointer-events-none"><path d="m6 9 6 6 6-6"></path></svg>
          </div>
        </div>
        
        <button @click="submit" type="submit" class="w-full py-2 bg-[#50B9E0] text-black border-none rounded-md font-medium cursor-pointer transition-colors hover:bg-[#3da5d4]">
          Submit Interest
        </button>
      </form>
    </div>

    <!-- Property Card -->
    <div class="bg-[#111111] rounded-xl p-6 w-full"
    :style="{ boxShadow: '0px 10px 60px 15px rgba(255, 255, 255, 0.4)' }"
    >
      <h2 class="text-xl font-semibold mb-6">Unit #1701</h2>
      
      <div class="swiper-container outer-swiper relative h-[18rem]"
      >
        <swiper
          :modules="[Pagination]"
          :pagination="{ clickable: true }"
          :slides-per-view="1.2"
          :space-between="10"
          class="rounded-lg"
          
        >
          <swiper-slide>
            <div class="relative w-full rounded-2xl h-[18rem] overflow-hidden">
              <video 
                class="w-[80vw] h-full object-cover"
                autoplay
                muted
                loop
                playsinline
              >
                <source src="/assets//videos//unit-video.mp4" type="video/mp4">
                Your browser does not support the video tag.
              </video>
              <div class="absolute inset-0 flex items-center justify-center">
                <button class="p-2 bg-opacity-50 rounded-full">
                  <img
                    src="assets/images/video-play.svg"
                    alt="video play"
                    class="w-[40px] sm:w-[60px]"
                  />
                </button>
              </div>
            </div>
          </swiper-slide>
          
          <swiper-slide v-for="(slide, index) in slides" :key="index">
            <img
              :src="slide"
              alt="Property Image" 
              class="w-full object-cover rounded-2xl h-[18rem]"
            />
          </swiper-slide>
        </swiper>
      </div>
      
      <div class="flex flex-col gap-3 mt-8 md:mt-4">
        <div class="flex items-center gap-2 text-sm text-[#cccccc]">
          <Icon name="line-md:home-simple-twotone" class="text-[rgba(242,249,253,0.7)]" />
          <span>Unit Type Name :asdf 2BHK</span>
        </div>
        <div class="flex items-center gap-2 text-sm text-[#cccccc]">
          <Icon name="famicons:apps-sharp" class="text-[rgba(242,249,253,0.7)]" />
          <span>Area : 1260 sq ft</span>
        </div>
        <div class="flex items-center gap-2 text-sm text-[#cccccc]">
          <Icon name="ph:bookmark-simple" class="text-[rgba(242,249,253,0.7)]" />
          <span>Units Available : 11</span>
        </div>
        <div class="flex items-center gap-2 text-sm text-[#cccccc]">
          <Icon name="material-symbols:calendar-month-outline" class="text-[rgba(242,249,253,0.7)]" />
          <span>Time for Completion : 11 mon</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { VueTelInput } from 'vue-tel-input';
import 'vue-tel-input/vue-tel-input.css';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/pagination';
import unit1 from "@/assets/images/units/unit1.png";
import unit2 from "@/assets/images/units/unit2.png";
import { Pagination } from "swiper/modules";
import MainSection from '~/components/VoiceInput.vue';

import { usePageLayoutStore } from '~/stores/pagelayoutStore';
const store = usePageLayoutStore();

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

const submit = () => {
  console.log('submitinterest')
  store.setLayout('/confirmation');
  // router.push("/confirmation");
};

const slides = [
  unit1,
  unit2
];

const formData = ref({
  fullName: '',
  email: '',
  contactNumber: '',
  unitNumber: '1702',
  brokerName: '',
  brokerAgency: ''
});

const submitForm = () => {
  console.log('Form submitted:', formData.value);
  // Here you would typically send the data to your backend
  alert('Interest registered successfully!');
};
</script>

<style scoped>
</style>