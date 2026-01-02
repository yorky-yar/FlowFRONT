<template>
  <div class="start-container">
    <div class="start-header">
      <div class="center-section">
        <div class="company-name">SILKBUDS</div>
      </div>
      
      <div class="right-section">
        <div class="menu-icon">
          <img src="@/assets/menu.svg" alt="Menu">
        </div>
      </div>
    </div>
    
    <div class="logo-circle"></div>
    <div class="rectangle-area">
      <div class="photo-slider">
        <div 
          class="slider-track"
          :style="{ transform: `translateX(-${currentPhotoIndex * 100}%)` }"
        >
          <div 
            v-for="(photo, index) in photos" 
            :key="index"
            class="slide"
          >
            <img 
              :src="photo" 
              alt="Фото букета" 
              class="slider-photo"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="text">Текст</div>
    <router-link to="/home" class="select-button">ВЫБРАТЬ БУКЕТ</router-link>
    <div class="scroll-bottom-spacer"></div>
  </div>
</template>

<script>
// Импортируем фотографии напрямую
import photo1 from '@/assets/photo-1.jpg'
import photo2 from '@/assets/photo-2.jpg'
import photo3 from '@/assets/photo-3.jpg'

export default {
  name: 'StartView',
  data() {
    return {
      currentPhotoIndex: 0,
      photos: [photo1, photo2, photo3],
      slideInterval: null
    }
  },
  mounted() {
    this.startSlider();
  },
  beforeUnmount() {
    this.stopSlider();
  },
  methods: {
    startSlider() {
      this.slideInterval = setInterval(() => {
        this.nextPhoto();
      }, 8000);
    },
    stopSlider() {
      if (this.slideInterval) {
        clearInterval(this.slideInterval);
      }
    },
    nextPhoto() {
      this.currentPhotoIndex = (this.currentPhotoIndex + 1) % this.photos.length;
    }
  }
}
</script>

<style scoped>
.start-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: white;
  padding-top: 30px;
  padding-bottom: 150px;
}

.start-header {
  width: 100%;
  height: 70px;
  background-color: #1c1B20;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
  padding-top: env(safe-area-inset-top, 0px);
}

.center-section {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.right-section {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 60px;
}

.company-name {
  font-size: 24px;
  font-weight: 500;
  color: white;
  text-align: center;
  letter-spacing: 0.5px;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

.menu-icon {
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.menu-icon img {
  width: 30px;
  height: 30px;
  object-fit: contain;
}

.logo-circle {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background-color: white;
  margin-top: 30px;
}

.rectangle-area {
  width: calc(100% - 200px);
  height: 450px;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 40px;
  margin-top: 60px;
  position: relative;
  overflow: hidden;
}

.photo-slider {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}

.slider-track {
  display: flex;
  height: 100%;
  transition: transform 1.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.slide {
  flex: 0 0 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.slider-photo {
  width: auto;
  height: 80%;
  max-width: 90%;
  object-fit: contain;
  border-radius: 20px;
}

.text {
  font-size: 28px;
  font-weight: 500;
  margin-top: 40px;
}

.select-button {
  width: 300px;
  height: 70px;
  background-color: rgba(255, 255, 255, 0.08);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 22px;
  font-weight: 500;
  color: white;
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-top: 40px;
  transition: all 0.3s ease;
}

.select-button:hover {
  background-color: rgba(255, 255, 255, 0.12);
  transform: translateY(-2px);
}

.scroll-bottom-spacer {
  height: 150px;
  width: 100%;
}

@media (max-width: 768px) {
  .start-header {
    height: 60px;
  }
  
  .company-name {
    font-size: 20px;
  }
  
  .menu-icon img {
    width: 28px;
    height: 28px;
  }
  
  .logo-circle {
    width: 100px;
    height: 100px;
  }
  
  .rectangle-area {
    width: calc(100% - 40px);
    height: 350px;
  }
  
  .slider-photo {
    height: 75%;
    max-width: 85%;
  }
  
  .text {
    font-size: 24px;
  }
  
  .select-button {
    width: 250px;
    height: 60px;
    font-size: 20px;
  }
}

@media (max-width: 480px) {
  .start-header {
    height: 56px;
  }
  
  .company-name {
    font-size: 18px;
  }
  
  .menu-icon img {
    width: 25px;
    height: 25px;
  }
  
  .logo-circle {
    width: 80px;
    height: 80px;
  }
  
  .rectangle-area {
    width: calc(100% - 40px);
    height: 280px;
  }
  
  .slider-photo {
    height: 70%;
    max-width: 80%;
  }
  
  .text {
    font-size: 20px;
  }
  
  .select-button {
    width: 200px;
    height: 50px;
    font-size: 18px;
  }
}
</style>