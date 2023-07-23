<script setup>
import { ref, reactive } from "vue";

const currentIndex = ref(0);
const images = reactive([
  {
    alt: "Green Forest",
    title: "Lush Green Forest Landscape",
    url: "https://images.pexels.com/photos/2233562/pexels-photo-2233562.jpeg",
    thumbnailUrl:
      "https://images.pexels.com/photos/2233562/pexels-photo-2233562.jpeg?h=100",
  },
  {
    alt: "Drinks",
    title: "Lemon lime soda",
    url: "https://images.pexels.com/photos/452737/pexels-photo-452737.jpeg",
    thumbnailUrl:
      "https://images.pexels.com/photos/452737/pexels-photo-452737.jpeg?h=100",
  },
  {
    alt: "A horse",
    title: "A horse in a ranch",
    url: "https://images.pexels.com/photos/1474114/pexels-photo-1474114.jpeg",
    thumbnailUrl:
      "https://images.pexels.com/photos/1474114/pexels-photo-1474114.jpeg?h=100",
  },
  {
    alt: "Pets",
    title: "Cat and Dog",
    url: "https://images.pexels.com/photos/6148103/pexels-photo-6148103.jpeg",
    thumbnailUrl:
      "https://images.pexels.com/photos/6148103/pexels-photo-6148103.jpeg?h=100",
  },
  {
    alt: "Cityscape at Night",
    title: "Cityscape at Night",
    url: "https://images.pexels.com/photos/4475925/pexels-photo-4475925.jpeg",
    thumbnailUrl:
      "https://images.pexels.com/photos/4475925/pexels-photo-4475925.jpeg?h=100",
  },
]);

const nextSlide = () => {
  currentIndex.value =
    currentIndex.value === images.length - 1 ? 0 : currentIndex.value + 1
};

const prevSlide = () => {
  currentIndex.value =
    currentIndex.value === 0 ? images.length - 1 : currentIndex.value - 1
}

const handleThumbnailClick = (index) => {
  currentIndex.value = index
}
</script>
<template>
  <!-- Carousel Container -->
  <div class="carousel-container">
    <!-- Carousel Slides -->
    <div class="carousel relative shadow-2xl bg-indigo-200">
      <div class="carousel-inner relative overflow-hidden w-2/3 mx-auto">
        <!-- Slide -->
        <template v-for="(image, index) in images" :key="index">
          <input
            :class="'carousel-open'"
            :type="'radio'"
            :id="'carousel-' + (index + 1)"
            name="carousel"
            :aria-hidden="true"
            hidden=""
            :checked="index === currentIndex"
          />
          <div :class="'carousel-item absolute opacity-0'" style="height: 75vh">
            <img
              :src="image.url"
              :alt="image.alt"
              :title="image.title"
              class="object-cover w-full h-full"
            />
          </div>
          <label
            class="w-10 h-10 ml-2 md:ml-10 absolute cursor-pointer text-3xl font-bold text-black hover:text-white rounded-full bg-white hover:bg-blue-300 leading-tight text-center z-10 inset-y-0 left-0 my-auto"
            @click.prevent="prevSlide"
            >‹</label
          >
          <label
            class="w-10 h-10 mr-2 md:mr-10 absolute cursor-pointer text-3xl font-bold text-black hover:text-white rounded-full bg-white hover:bg-blue-300 leading-tight text-center z-10 inset-y-0 right-0 my-auto"
            @click.prevent="nextSlide"
            >›</label
          >
        </template>
      </div>
      <!-- Carousel Indicators -->
      <ol class="carousel-indicators">
        <li
          v-for="(image, index) in images"
          :key="index"
          class="inline-block mr-3"
        >
          <label
            class="carousel-bullet cursor-pointer block text-4xl text-white hover:text-indigo-300"
            @click="handleThumbnailClick(index)"
          >
            •
          </label>
        </li>
      </ol>
    </div>

    <!-- Carousel Thumbnails -->
    <div class="carousel-thumbnails mt-5">
      <template v-for="(image, index) in images" :key="index">
        <label class="carousel-thumbnail cursor-pointer inline-block mr-3">
          <img
            :src="image.thumbnailUrl"
            :alt="image.alt"
            :title="image.title"
            class="w-16 h-12 object-cover border border-gray-300"
            @click="handleThumbnailClick(index)"
          />
        </label>
      </template>
    </div>
  </div>
</template>

<style scoped>
.carousel {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Thumbnails */
.carousel-thumbnails {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 15px;
  /* Add some space between the slider and thumbnails */
}

.carousel-thumbnail {
  cursor: pointer;
  transition: opacity 0.3s;
}

.carousel-thumbnail img:hover {
  opacity: 0.7;
}

.carousel-open:checked + .carousel-item {
  position: static;
  opacity: 100;
}

.carousel-item {
  -webkit-transition: opacity 0.6s ease-out;
  transition: opacity 0.6s ease-out;
}

#carousel-1:checked ~ .control-1,
#carousel-2:checked ~ .control-2,
#carousel-3:checked ~ .control-3 {
  display: block;
}

.carousel-indicators {
  list-style: none;
  margin: 0;
  padding: 0;
  position: absolute;
  bottom: 2%;
  left: 0;
  right: 0;
  text-align: center;
  z-index: 10;
}

#carousel-1:checked
  ~ .control-1
  ~ .carousel-indicators
  li:nth-child(1)
  .carousel-bullet,
#carousel-2:checked
  ~ .control-2
  ~ .carousel-indicators
  li:nth-child(2)
  .carousel-bullet,
#carousel-3:checked
  ~ .control-3
  ~ .carousel-indicators
  li:nth-child(3)
  .carousel-bullet {
  color: #ffb317;
}
</style>
