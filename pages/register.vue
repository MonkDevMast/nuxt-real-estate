<template>
    <img src="../assets/images//layout-bg.png" class="absolute inset-0 top-0 left-0 w-full h-full object-cover"/>
  
    <div class="flex flex-col min-h-screen items-center text-white font-sans relative">
      <!-- Header -->
      <HeaderRegister />
      <!-- Mobile Layout (form first, then card) -->
      <MobileRegister />
      <!-- Desktop Layout (original layout) -->
       <DesktopRegister />
      <!-- Footer (Desktop only) -->
       <FooterRegister />
     </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  import MobileRegister from '~/pages/register/Mobile.vue';
  import DesktopRegister from '~/pages/register/Desktop.vue';
  import FooterRegister from '~/pages/register/Footer.vue';
  import HeaderRegister from '~/pages/register/Header.vue';
  
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

  const formData = ref({
    fullName: '',
    email: '',
    contactNumber: '',
    unitNumber: '1702',
    brokerName: '',
    brokerAgency: ''
  });

  </script>
  
  <style scoped>
  .swiper {
    padding-bottom: 30px; /* Space for pagination */
  }

  .form {
  box-shadow: 0px 10px 60px 15px rgba(255, 255, 255, 0.6);
  width: 70vw;
}

@media (max-width: 768px) {
  .form {
    box-shadow: none;
    width: 100vw;
  }
  
  /* Hide scrollbar but keep functionality */
  .md\:hidden::-webkit-scrollbar {
    display: none;
  }
  
  .md\:hidden {
    -ms-overflow-style: none;
    scrollbar-width: none;
  }
}

.outer-mobile-swiper .swiper-pagination {
  background-color: red;
}
  
  .outer-swiper .swiper-pagination-bullet.swiper-pagination-bullet-active,
  .outer-mobile-swiper .swiper-pagination-bullet.swiper-pagination-bullet-active {
    background: #33c3f0;
  }
  
  .mobile-inner-swiper.swiper .swiper-pagination {
    display: flex;
  }
  
  .outer-swiper .swiper-pagination,
  .outer-mobile-swiper .swiper-pagination {
    position: absolute;
    bottom: -40px;
    left: 0;
    right: 0;
    text-align: center;
    display: flex;
    justify-content: start;
    align-items: center;
  }
  
  .outer-swiper .swiper-pagination-bullet,
  .outer-mobile-swiper .swiper-pagination-bullet {
    background: #5c5c5c;
    width: 37.257px;
    height: 5.29px;
    border-radius: 49.633px;
    opacity: 1;
  }
  
  .mobile-inner-swiper .swiper-pagination-bullet {
    background: #000;
    width: 30.257px;
    height: 5.29px;
    border-radius: 49.633px;
    opacity: 1;
  }
  
  .outer-swiper .swiper-slide-active .inner-swiper .swiper-pagination-bullet {
    background: rgba(121, 121, 121, 0.3) !important;
  }
  
  .outer-swiper
    .swiper-slide-active
    .inner-swiper
    .swiper-pagination-bullet.swiper-pagination-bullet-active {
    background: #33c3f0 !important;
  }
  
  .inner-swiper .swiper-pagination-bullet {
    background: #000;
    width: 37.257px;
    height: 5.29px;
    border-radius: 49.633px;
    opacity: 1;
  }
   
  .swiper-slide {
    transition: transform 0.3s ease;
  }
  
  /* Mobile specific styles */
  @media (max-width: 767px) {
    .swiper-container {
      height: 18rem !important;
    }
    
    .swiper-slide {
      height: 18rem !important;
    }
    
    .video-container {
      height: 18rem !important;
    }
    
    /* Show icons on mobile */
    .mobile-icon {
      display: block !important;
    }
  }

  .outer-swiper .swiper-pagination, .outer-mobile-swiper .swiper-pagination  {
    justify-content: start !important;
  }
  </style>