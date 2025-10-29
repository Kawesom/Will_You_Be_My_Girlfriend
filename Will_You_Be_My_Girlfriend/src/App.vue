<template>

  <body class="bg-pink-200" style="height: 100vh;">
    <div v-if="confetti" v-confetti="{ particleCount: 200, force: 0.5, duration: 5000, stageWidth: 3000 }" />
    <!--
    <swiper @swiper="onSwiper" class="mySwiper" :slides-per-view="5" :space-between="30"
          :autoplay="{ delay: 2000, disableOnInteraction: false }" :modules="[Autoplay, Virtual]" virtual>
      <swiper-slide style="transition-timing-function: linear !important;" v-for="(pic, index) in pics" :key="index" :virtualIndex="index">
        <img :src="pic" width="20%" height="100%" alt="GF pics" style="object-fit: cover;" />
      </swiper-slide>
    </swiper>-->
    <div class="flex max-w-100% min-h-100vh flex-wrap">
      <video v-for="v of vids" :key="v" height="100%" autoplay loop muted playsinline class="lg:w-1/5 w-full">
        <source :src="v" type="video/mp4">
      </video>
    </div>

    <!-- The Modal -->
    <div id="myModal" ref="modal" class="modal">

      <!-- Modal content -->
      <div class="modal-content">
        <span class="close" ref="span" @click="spanClick">&times;</span>
        <p>To the Biggest Drama Queen,</p>
        <p>Everyone's Fashion Queen,</p>
        <p>And the most beautiful darkskin Queen.</p>
        <p>You bring a certain light to the lives of all the people you come in contact with and I hope you'll bring that same light to my life moving forward.</p>
        <p style="font-size:larger; font-weight:bold; margin-top: 2%;">Angel Oghenemine Iroro, </p>
        <p style="font-size:x-large; font-weight:bold; margin-top: 2%; text-align:center;">Will you be my Girlfriend?</p>
        <div style="display: flex; justify-content: center; gap: 20px; margin-top: 3%;">
          <button class="hover:underline py-2" @click="stop">No</button>
          <button class="hover:underline py-2" @click="start">Yes</button>
        </div>
        <p style="text-align: center;" v-show="display">🤣For Where? You're stuck with me Fam</p>
        <p style="text-align:end;">Love, Kamal</p>
      </div>

    </div>

  </body>
</template>

<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Autoplay, Virtual } from 'swiper/modules';
import { onMounted, ref } from 'vue';
import { vConfetti } from '@neoconfetti/vue';

const slides = ref(null);
const vids = ref([]);
const pics = ref([]);
const modal = ref(null);
const span = ref(null);
const confetti = ref(false);
const display = ref(false);

const makeVidArray = () => {
  /*for (let i = 30; i < 42; i++) {
    vids.value.push(`/media/${i}.mp4`);
  }*/ // Same as below

  Array.from({ length: 15 }, (_, i) => vids.value.push(`https://github.com/Kawesom/Will_You_Be_My_Girlfriend/raw/refs/heads/main/Will_You_Be_My_Girlfriend/public/media/${i + 30}.mp4`));
};

const makePicArray = () => {
  /*for (let i = 1; i < 30; i++) {
    pics.value.push(`/media/${i + 1}.jpg`)
  }*/ // Same as below

  Array.from({ length: 29 }, (_, i) => pics.value.push(`https://github.com/Kawesom/Will_You_Be_My_Girlfriend/raw/refs/heads/main/Will_You_Be_My_Girlfriend/public/media/${i + 1}.jpg`));
};

const onSwiper = (swiper) => {
  console.log("Slides", swiper);
  slides.value = swiper;
};


const start = () => {
  confetti.value = true;
  modal.value.style.display = "none";
  setTimeout(() => {
    confetti.value = false;
  }, 5000);
}

const stop = () => {
  display.value = true;
  setTimeout(() => {
    display.value = false;
  }, 2000);
}

// When the user clicks on <span> (x), close the modal
const spanClick = () => {
  modal.value.style.display = "none";
}

// When the user clicks anywhere outside of the modal, close it
window.onclick = function(event) {
  if (event.target == modal.value) {
    modal.value.style.display = "none";
  }
}

onMounted(() => {
  makeVidArray();
  makePicArray();
  setTimeout(() => {
    modal.value.style.display = "block";
  }, 500);
});

</script>

<style scoped>

.mySwiper {
    color: black;
    height: 100%;
    width: 100%;
    transition-timing-function: linear;
}

body {
  font-family: 'Lugrasimo', cursive, sans-serif;
}

/* The Modal (background) */
.modal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}

/* The Close Button */
.close {
  color: #aaaaaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}

</style>
