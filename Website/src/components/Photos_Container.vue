<template>
    <div class="photos-container">
      <!-- Modal -->
      <div v-if="activeAlbum" class="modal" @click.self="closeAlbum">
        <div class="modal-content">
          <button class="close-button" @click="closeAlbum">X</button>

          <h2 class="album-title">{{ activeAlbum.title }}</h2>
  
          <div class="carousel">
            <button class="prev-button" @click="prevImage">‹</button>
            <img :src="activeAlbum.photos[currentIndex]" alt="Photo" />
            <button class="next-button" @click="nextImage">›</button>
          </div>
        </div>
      </div>
  
      <!-- Albums -->
      <div
        v-for="(album, index) in albums"
        :key="index"
        :class="['album', index % 2 === 0 ? 'left' : 'right']"
        @click="openAlbum(album)"
      >
        <h2>{{ album.title }}</h2>
        <p>
          <font-awesome-icon icon="location-dot" /> {{ album.cidade }}
        </p>
        <p>
          <font-awesome-icon icon="calendar" /> {{ album.data }}
        </p>
        <p v-if="album.distancia">
          <font-awesome-icon icon="check" /> {{ album.distancia }}
        </p>
        <p v-if="album.tempo">
          <font-awesome-icon icon="clock" /> {{ album.tempo }}
        </p>
      </div>
    </div>
  </template>
  
  
  <script>
    import { Swiper, SwiperSlide } from "swiper/vue";
    import {Navigation, Pagination, Scrollbar } from "swiper/modules";


    import { library } from "@fortawesome/fontawesome-svg-core";
    import { faLocationDot, faCalendar,faCheck,faClock } from "@fortawesome/free-solid-svg-icons";
    import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

library.add(faLocationDot, faCalendar,faCheck,faClock);

  // Import Swiper styles
  import "swiper/css";
  import "swiper/css/navigation";
  import "swiper/css/pagination";
  import "swiper/css/scrollbar";
  
  export default {
    name: "PhotosContainer",
    components: {
        Swiper,
        SwiperSlide,
        FontAwesomeIcon,
    },
    props: {
      isDarkMode: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        albums: [
          {
            title: "Miles & Vibes Runs",
            cidade:"Portugal",
            data:"Sometimes",
            photos: [
                "/images/Miles/image1.jpeg",
                "/images/Miles/image2.jpeg",
                "/images/Miles/image3.jpeg",
                "/images/Miles/image4.jpeg",
                "/images/Miles/image5.jpeg",
                "/images/Miles/image6.jpeg",
                "/images/Miles/image7.jpeg",
                ],

          },
          {
            title: "Meia Maratona Sunset",
            cidade:"Caminha",
            data:"14-06-2024",
            distancia:"21,1km",
            tempo:"1:59:25",
            photos: [
                "/images/Sunset2024/image1.jpeg",
                "/images/Sunset2024/image2.jpeg",
                "/images/Sunset2024/image3.jpeg",
                "/images/Sunset2024/image4.jpeg",
                "/images/Sunset2024/image5.jpeg",
                "/images/Sunset2024/image6.jpeg",
                "/images/Sunset2024/image7.jpeg",
                "/images/Sunset2024/image8.jpeg",
                "/images/Sunset2024/image9.jpeg",
                "/images/Sunset2024/image10.jpeg",
                ],

          },
          {
            title: "Meia Maratona do Porto",
            cidade:"Porto",
            data:"16-09-2024",
            distancia:"21,1km",
            tempo:"1:38:48",
            photos: [
                "/images/MeiaPorto/image1.jpg",
                "/images/MeiaPorto/image2.jpeg",
                "/images/MeiaPorto/image3.jpeg",
                "/images/MeiaPorto/image4.jpeg",
                "/images/MeiaPorto/image5.jpeg",
                "/images/MeiaPorto/image6.jpeg",
                "/images/MeiaPorto/image7.jpeg",
                "/images/MeiaPorto/image8.jpeg",
                "/images/MeiaPorto/image9.jpeg",
                ],
          },
          {
            title: "Corrida da Ponte",
            cidade:"Viana do Castelo",
            data:"13-10-2024",
            distancia:"10km",
            tempo:"44:45",
            photos: [
                "/images/Ponte2024/image1.jpg",
                "/images/Ponte2024/image2.jpeg",
                "/images/Ponte2024/image3.jpeg",
                "/images/Ponte2024/image4.jpeg",
               
                ],
          },
          {
            title: "S. Silvestre",
            cidade:"Viana do Castelo",
            data:"27-12-2024",
            distancia:"10km",
            tempo:"49:51",
            photos: [
                "/images/SSilvestreV2024/image1.jpeg",
                "/images/SSilvestreV2024/image2.jpeg",
                ],
          },
          {
            title: "Meia Maratona Manuela Machado",
            cidade:"Viana do Castelo",
            data:"19-01-2025",
            distancia:"21,1km",
            tempo:"1:51:10",
            photos: [
              "/images/MMMM2025/Image1.jpeg",
            ],
          },
        ],
        activeAlbum: null,
        currentIndex: 0,
      };
    },
    computed: {
      themeClass() {
        return this.isDarkMode ? "dark" : "light";
      },
    },
    methods: {
    openAlbum(album) {
      this.activeAlbum = album;
      this.currentIndex = 0; // Reset to the first image
    },
    closeAlbum() {
      this.activeAlbum = null;
    },
    nextImage() {
      if (this.activeAlbum) {
        this.currentIndex = (this.currentIndex + 1) % this.activeAlbum.photos.length;
      }
    },
    prevImage() {
      if (this.activeAlbum) {
        this.currentIndex =
          (this.currentIndex - 1 + this.activeAlbum.photos.length) % this.activeAlbum.photos.length;
      }
    },
  },
  }
  </script>
  
  <style scoped>
  .photos-container {
    width: 60%;
    height: 70%;
    margin: 0 auto;
    margin-top: 23vh;
    display: flex;
    flex-direction: column;
    gap: 25px;
    align-items: center;
    margin-bottom: 2rem;
  }
  
  .album {
    width: 90%;
    padding: 20px 30px;
    font-size: 1.2rem;
    color: white;
    border-radius: 50px;
    text-align: center;
    background-color: #2d3436;
    background-image: linear-gradient(315deg, #2d3436 0%, #000000 74%);
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .album-title {
  font-size: 1.2rem;
  font-weight: bold;
  margin-top: 50px;
  text-align: center;
  color: #333;
}

  .album p{
    font-size: 1rem;
  }
  
  .album:hover {
    background-color: #444;
  }
  
  .album.left {
    text-align: left;
  }
  
  .album.right {
    text-align: right;
  }
  
  .modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  width: 80%;
  max-width: 1000px;
  height: 80vh;
  background: transparent;
  border-radius: 10px;
  padding: 20px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  overflow: hidden; /* Garante que o conteúdo não ultrapasse os limites */
}

.carousel {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  position: relative;
}

.carousel img {
  max-height: 90%;
  max-width: 90%;
  object-fit: contain; /* Mantém a proporção sem distorcer a imagem */
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5);
}

.prev-button,
.next-button {
  background: rgba(0, 0, 0, 0.5);
  border: none;
  font-size: 2rem;
  color: #fff;
  cursor: pointer;
  padding: 5px 10px;
  margin: 0 10px;
  border-radius: 20%;
  z-index: 2; /* Garantir que os botões fiquem acima da imagem */
}

.prev-button:hover,
.next-button:hover {
  background: rgba(0, 0, 0, 0.8);
}

.close-button {
  position: absolute;
  top: 20px;
  right: 15px;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: white;
  z-index: 1001;
}

.close-button:hover {
  color: #555;
}

  @media (max-width: 768px) {
  .photos-container {
    width: 80%;
  }

  .album {
    width: 90%;
    padding: 20px 20px;
    font-size: 0.8rem;
    justify-content: center;
    color: white;
    border-radius: 50px;
    text-align: center;
    background-color: #2d3436;
    background-image: linear-gradient(315deg, #2d3436 0%, #000000 74%);
    cursor: pointer;
    transition: background-color 0.3s ease;
  }



}
  </style>
  