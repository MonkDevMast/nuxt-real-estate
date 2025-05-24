<script setup lang="ts">
import { useRouter } from "vue-router";
import { ref, onMounted } from "vue";
import { computed } from 'vue';

import SwiperDesktop from "~/components/Swiper/Desktop.vue";
import SwiperMobile from "~/components/Swiper/Mobile.vue";

definePageMeta({
  layout: 'default',
});

const router = useRouter();

useHead({
  title: "Rechitta - Property List",
  meta: [
    {
      name: "description",
      content:
        "Discover, explore, and seal deals on premium properties with ease. Your next home or investment is just a click away.",
    },
  ],
});

const isLoading = ref(true);
const isExpanded = ref(false);
const expanded = ref(false);
const paginationVisible = computed(() => !isExpanded.value);
const outerSwiperRef = ref<any>(null);
const outerMobileSwiperRef = ref<any>(null);

// Video control refs and state
const videoRefs = ref<HTMLVideoElement[]>([]);
const videoStates = ref<{isPlaying: boolean, hovered: boolean}[]>([]);

const goToProperty = (i: number) => {
  
  const swiper = outerSwiperRef.value?.swiper;
  if (swiper) {
    swiper.allowTouchMove = false;
    swiper.mousewheel.disable();
  }

  // Pause all videos when expanding
  expanded.value = true
  isExpanded.value = true
  videoRefs.value.forEach((video, index) => {
    if (video) {
      video.pause();
      if (videoStates.value[index]) {
        videoStates.value[index].isPlaying = false;
      }
    }
  });
  
  const outerSwiper = document.querySelector(".outer-swiper.swiper") as HTMLElement;
  if (!outerSwiper) return;

  const prevSlide = outerSwiper.querySelector(
    ":scope > .swiper-wrapper > .swiper-slide-prev"
  );
  const nextSlide = outerSwiper.querySelector(
    ":scope > .swiper-wrapper > .swiper-slide-next"
  );
  const activeSlide = outerSwiper.querySelector(
    ":scope > .swiper-wrapper > .swiper-slide-active"
  );

  prevSlide?.classList.add("slide-out-left");
  nextSlide?.classList.add("slide-out-right");
  activeSlide?.classList.add("slide-up");

  setTimeout(() => {
    isExpanded.value = true;
    activeSlide?.classList.add("expanded");
    outerSwiper.classList.add("expanded");
    
    outerSwiper.style.marginBottom = "-80px";
    const pagination = outerSwiper.querySelector('.swiper-pagination') as HTMLElement;
    if (pagination) {
      pagination.style.display = 'none';
    }
  }, 600);
};

const collapseView = () => {
  const swiper = outerSwiperRef.value?.swiper;
  if (swiper) {
    swiper.allowTouchMove = true;
    swiper.mousewheel.enable();
  }
  // Pause all videos when collapsing
  expanded.value = false
  videoRefs.value.forEach((video, index) => {
    if (video) {
      video.pause();
      if (videoStates.value[index]) {
        videoStates.value[index].isPlaying = false;
      }
    }
  });

  const outerSwiper = document.querySelector(".outer-swiper.swiper") as HTMLElement;
  if (!outerSwiper) return;

  // Add transition to both detail cards
  const detailCards = document.querySelectorAll(".detail-card") as NodeListOf<HTMLElement>;
  detailCards.forEach(card => {
    card.style.transition = "transform 0.6s ease, opacity 0.5s ease";
    card.style.transform = "translateY(100px)";
    card.style.opacity = "0";
  });

  setTimeout(() => {
    const prevSlide = outerSwiper.querySelector(
      ":scope > .swiper-wrapper > .swiper-slide-prev"
    );
    const nextSlide = outerSwiper.querySelector(
      ":scope > .swiper-wrapper > .swiper-slide-next"
    );
    const activeSlide = outerSwiper.querySelector(
      ":scope > .swiper-wrapper > .swiper-slide-active"
    );

    prevSlide?.classList.remove("slide-out-left");
    nextSlide?.classList.remove("slide-out-right");
    activeSlide?.classList.remove("slide-up");
    activeSlide?.classList.remove("expanded");
    outerSwiper.classList.remove("expanded");

    activeSlide?.classList.add("slide-down");

    const pagination = outerSwiper.querySelector('.swiper-pagination') as HTMLElement;
    if (pagination) {
      pagination.style.display = 'flex';
    }

    outerSwiper.style.marginBottom = "0";

    setTimeout(() => {
      activeSlide?.classList.remove("slide-down");
      isExpanded.value = false;
    }, 400);
  }, 400);
};

watch(expanded, (newVal) => {
  const swiper = outerSwiperRef.value?.swiper;
  if (!swiper) return;

  swiper.allowTouchMove = !newVal;
  
  swiper.updateSize();
  swiper.updateSlides();
  
  swiper.mousewheel.disable();
  if (!newVal) swiper.mousewheel.enable();
});

// fetch data from backend
const realEstateDatas = ref([
  {
    var: '2BHK - Corner Unit',
    view: 'Full Burj Khalifa + Downtown Skyline',
    unit: '1902',
    size: '1260 sq ft',
    floor: 'Floor 11',
    price: 'AED 2,150,000',
    features: [
      'Smart Home Automation',
      'Spacious Balcony',
      'Premium Finishes',
      'Concierge Access',
      'Double Glazed Windows',
    ],
    bedrooms: '2',
    bathrooms: '2',
  },
  {
    var: '2BR Duplex',
    view: 'Pool-Facing Premium',
    unit: '1905',
    size: '1560 sq ft',
    floor: 'Podium Floor 2',
    price: 'AED 2,150,000',
    features: [
      'Double-height Ceiling',
      'Private Balcony',
      'Walk-In Closet',
      'Smart Entry System',
      'Direct Amenity Access',
    ],
    bedrooms: '2',
    bathrooms: '2',
  },
  {
    var: '2BR Duplex',
    view: 'Pool-Facing Premium',
    unit: '1901',
    size: '1560 sq ft',
    floor: 'Podium Floor 2',
    price: 'AED 2,150,000',
    features: [
      'Double-height Ceiling',
      'Private Balcony',
      'Walk-In Closet',
      'Smart Entry System',
      'Direct Amenity Access',
    ],
    bedrooms: '2',
    bathrooms: '2',
  }
]);
</script>

<template>
  <div class="h-full flex flex-col !ml-2 md:ml-0 justify-center items-center relative">
    <!-- Loading overlay -->
    <transition name="fade">
      <div v-if="isLoading" class="">
        <!-- <div class="loading-spinner"></div> -->
      </div>
    </transition>

    <!-- Main content container -->
    <div class="w-full flex-1 flex flex-col items-center justify-center relative ">
      <!-- Swiper container -->
      <div :class="`w-full h-50 flex  items-center justify-center relative `">
        <!-- Desktop Swiper -->
        <SwiperDesktop
          @collapseview="collapseView"
          @goToProperty="goToProperty"
          :datas="realEstateDatas"
          v-model:isExpanded="isExpanded"
          />

        <!-- Mobile Swiper -->
        <SwiperMobile
          @collapseview="collapseView"
          @goToProperty="goToProperty"
          :datas="realEstateDatas"
          v-model:isExpanded="isExpanded"
          />
      </div>
    </div>
    </div>
   
    <div class="flex justify-center relative bottom-[15rem] mb-44 md:bottom-32">
      <transition name="fade-slide">
        <div 
          v-if="isExpanded" 
          class="w-full max-w-[1300px] md:w-[73rem] px-4 mt-5 relative mb-10"
        >
          <!-- Mid Card -->
          <div 
            :style="{ boxShadow: '0px 0px 150px 0px rgba(167, 167, 167, 0.5)' }"
            class="hide-scrollbar flex text-white gap-6 bg-black backdrop-blur-xl rounded-3xl shadow-lg py-8 px-4 sm:py-9 pr-8 md:px-9 w-full overflow-x-auto overflow-y-hidden whitespace-nowrap scroll-smooth transition-all duration-300 ease-in-out relative detail-card text-xs sm:text-sm mb-8"
          >
            <div class="flex items-center gap-1 flex-shrink-0">
              <Icon name="line-md:home-simple-twotone" class="text-[rgba(242,249,253,0.7)] hidden sm:block" />
              <span class="text-[rgba(242,249,253,0.7)]">Unit Type Name : <span class="text-white">2BHK</span></span>
            </div>
            <div class="flex items-center gap-1 flex-shrink-0">
              <Icon name="famicons:apps-sharp" class="text-[rgba(242,249,253,0.7)] hidden sm:block" />
              <span class="text-[rgba(242,249,253,0.7)]">Area : <span class="text-white">1,260 sq ft</span></span>
            </div>
            <div class="flex items-center gap-1 flex-shrink-0">
              <Icon name="ph:bookmark-simple" class="text-[rgba(242,249,253,0.7)] hidden sm:block" />
              <span class="text-[rgba(242,249,253,0.7)]">Units Available : <span class="text-white">11</span></span>
            </div>
            <div class="flex items-center gap-1 flex-shrink-0">
              <Icon name="material-symbols:calendar-month-outline" class="text-[rgba(242,249,253,0.7)] hidden sm:block" />
              <span class="text-[rgba(242,249,253,0.7)]">Time for Completion : <span class="text-white">11 months</span></span>
            </div>
            <div class="flex items-center gap-1 flex-shrink-0">
              <Icon name="ph:sun" class="text-[rgba(242,249,253,0.7)] hidden sm:block" />
              <span class="text-[rgba(242,249,253,0.7)]">View : <span class="text-white">Burj View</span></span>
            </div>
          </div>

          <!-- Map Section -->
          <div
            :style="{ boxShadow: '0px 10px 60px 15px rgba(255, 255, 255, 0.4)' }"
            class="flex flex-col bg-black backdrop-blur-xl rounded-3xl shadow-lg p-9 w-full overflow-hidden transition-all duration-300 ease-in-out relative detail-card"
          >
            <div class="text-white w-full text-2xl mb-4 max-h-[15%] flex items-center justify-between gap-2 sm:gap-0">
              Location
            </div>
            <div class="w-full h-[400px]">
              <iframe
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3609.249543689662!2d55.2707823150116!3d25.20484928389806!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3e5f434570f1c4e3%3A0x403f651eba6edc8!2sBurj%20Khalifa!5e0!3m2!1sen!2sae!4v1616857199386!5m2!1sen!2sae"
                class="h-full w-full"
                style="border: 0; border-radius: 16px"
                allowfullscreen="true"
                loading="lazy"
                referrerpolicy="no-referrer-when-downgrade"
              ></iframe>
            </div>
          </div>
        </div>
      </transition>
    </div>
</template>

<style >

</style>