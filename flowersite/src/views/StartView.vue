<template>
  <div class="start-container" ref="container">
    <div class="start-header" :class="{ 'scrolled': isScrolled }">
      <div class="center-section">
        <div class="company-name">SILKBUDS</div>
      </div>
      
      <div class="right-section">
        <div class="menu-icon" @click="toggleMenu">
          <img src="@/assets/menu.svg" alt="Menu">
        </div>
      </div>
    </div>
    
    <transition name="slide-left">
      <div v-if="isMenuOpen" class="dropdown-menu" @click="closeMenu">
        <div class="dropdown-content" @click.stop>
          <div class="dropdown-header">
            <div class="dropdown-title">МЕНЮ</div>
            <div class="dropdown-close" @click="closeMenu">✕</div>
          </div>
          
          <div class="dropdown-items">
            <div class="dropdown-item" @click="navigateTo('home')">Выбор букета</div>
            <div class="dropdown-item" @click="navigateTo('tariffs')">Тарифы доставки</div>
            <div class="dropdown-item" @click="navigateTo('sales')">Акции</div>
            <div class="dropdown-item" @click="navigateTo('contacts')">Наши контакты</div>
          </div>
        </div>
      </div>
    </transition>
    
    <div class="logo-circle"></div>
    <div class="rectangle-area">
      <div class="photo-slider">
        <div 
          class="slider-track"
          :style="{ transform: `translateX(-${currentPhotoIndex * 100}%)`, transition: isTransitioning ? 'transform 1.5s cubic-bezier(0.4, 0, 0.2, 1)' : 'none' }"
          @transitionend="onTransitionEnd"
        >
          <div 
            v-for="(photo, index) in sliderPhotos" 
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
import photo1 from '@/assets/photo-1.jpg'
import photo2 from '@/assets/photo-2.jpg'
import photo3 from '@/assets/photo-3.jpg'

export default {
  name: 'StartView',
  data() {
    return {
      currentPhotoIndex: 0,
      isTransitioning: true,
      photos: [photo1, photo2, photo3],
      slideInterval: null,
      isMenuOpen: false,
      isScrolled: false,
      lastScrollPosition: 0,
      scrollTimeout: null
    }
  },
  computed: {
    sliderPhotos() {
      return [...this.photos, this.photos[0]];
    }
  },
  mounted() {
    this.startSlider();
    document.documentElement.scrollTop = 0;
    document.body.scrollTop = 0;
    
    this.$nextTick(() => {
      if (this.$refs.container) {
        this.$refs.container.scrollTop = 0;
        this.$refs.container.addEventListener('scroll', this.handleScroll);
      }
    });
  },
  beforeUnmount() {
    this.stopSlider();
    if (this.scrollTimeout) clearTimeout(this.scrollTimeout);
    if (this.$refs.container) {
      this.$refs.container.removeEventListener('scroll', this.handleScroll);
    }
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
      this.isTransitioning = true;
      this.currentPhotoIndex = (this.currentPhotoIndex + 1) % this.sliderPhotos.length;
    },
    onTransitionEnd() {
      if (this.currentPhotoIndex === this.sliderPhotos.length - 1) {
        this.isTransitioning = false;
        this.currentPhotoIndex = 0;
      }
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    closeMenu() {
      this.isMenuOpen = false;
    },
    navigateTo(route) {
      this.closeMenu();
      if (this.$route.name !== route) {
        this.$router.push({ name: route });
      }
    },
    handleScroll() {
      if (this.$refs.container) {
        const currentScrollPosition = this.$refs.container.scrollTop;
        this.isScrolled = currentScrollPosition > 50;
        
        if (this.isMenuOpen) {
          if (this.scrollTimeout) clearTimeout(this.scrollTimeout);
          
          this.scrollTimeout = setTimeout(() => {
            if (currentScrollPosition > this.lastScrollPosition + 30) {
              this.closeMenu();
            }
            this.lastScrollPosition = currentScrollPosition;
          }, 50);
        }
      }
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
  position: relative;
  overflow-anchor: none;
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
  position: sticky;
  top: 0;
  z-index: 100;
  transition: background-color 0.3s ease;
}

.start-header.scrolled {
  background-color: rgba(28, 27, 32, 0.95);
  backdrop-filter: blur(10px);
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
  cursor: pointer;
  transition: transform 0.3s ease;
}

.menu-icon:hover {
  transform: scale(1.1);
}

.menu-icon img {
  width: 30px;
  height: 30px;
  object-fit: contain;
}

.dropdown-menu {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  width: 33.333%;
  min-width: 300px;
  background-color: rgba(28, 27, 32, 0.9);
  border-left: 1px solid rgba(255, 255, 255, 0.2);
  z-index: 2000;
  display: flex;
  flex-direction: column;
}

.dropdown-content {
  width: 100%;
  height: 100%;
  padding: 40px;
  display: flex;
  flex-direction: column;
}

.dropdown-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 60px;
}

.dropdown-title {
  font-size: 24px;
  font-weight: 600;
  color: white;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.dropdown-close {
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 28px;
  color: white;
  cursor: pointer;
  border-radius: 50%;
  transition: background-color 0.3s ease;
}

.dropdown-close:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.dropdown-items {
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.dropdown-item {
  font-size: 18px;
  color: white;
  padding: 15px 20px;
  border-radius: 15px;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  padding-left: 0;
}

.dropdown-item:hover {
  background-color: rgba(255, 255, 255, 0.1);
  transform: translateX(10px);
}

.dropdown-item::before {
  content: '›';
  position: absolute;
  right: 20px;
  opacity: 0;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.dropdown-item:hover::before {
  opacity: 1;
  transform: translateX(5px);
}

.slide-left-enter-active,
.slide-left-leave-active {
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.slide-left-enter-from,
.slide-left-leave-to {
  opacity: 0;
  transform: translateX(100%);
}

.slide-left-enter-to,
.slide-left-leave-from {
  opacity: 1;
  transform: translateX(0);
}

.logo-circle {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background-color: white;
  margin-top: 30px;
}

.rectangle-area {
  width: calc(100% - 80px);
  max-width: 1600px;
  height: 700px;
  background-color: transparent;
  margin-top: 60px;
  position: relative;
  overflow: hidden;
}

.photo-slider {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  border-radius: 40px;
}

.slider-track {
  display: flex;
  height: 100%;
}

.slide {
  flex: 0 0 100%;
  min-width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.slider-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  display: block;
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

@media (max-width: 1200px) {
  .rectangle-area {
    height: 600px;
  }
}

@media (max-width: 992px) {
  .rectangle-area {
    height: 500px;
  }
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
  
  .dropdown-menu {
    width: 100%;
    min-width: unset;
  }
  
  .dropdown-content {
    padding: 30px;
  }
  
  .dropdown-title {
    font-size: 20px;
  }
  
  .dropdown-close {
    width: 40px;
    height: 40px;
    font-size: 24px;
  }
  
  .dropdown-item {
    font-size: 16px;
    padding: 12px 15px;
  }
  
  .logo-circle {
    width: 100px;
    height: 100px;
  }
  
  .rectangle-area {
    width: calc(100% - 40px);
    height: 400px;
  }
  
  .photo-slider {
    border-radius: 30px;
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

@media (max-width: 576px) {
  .rectangle-area {
    height: 300px;
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
  
  .dropdown-content {
    padding: 25px;
  }
  
  .dropdown-title {
    font-size: 18px;
  }
  
  .dropdown-close {
    width: 35px;
    height: 35px;
    font-size: 20px;
  }
  
  .dropdown-item {
    font-size: 15px;
    padding: 10px 12px;
  }
  
  .logo-circle {
    width: 80px;
    height: 80px;
  }
  
  .rectangle-area {
    width: calc(100% - 40px);
    height: 250px;
  }
  
  .photo-slider {
    border-radius: 20px;
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