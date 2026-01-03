<template>
  <div class="order-view">
    <div class="order-header">
      <div class="back-button" @click="goBack">
        <img src="@/assets/arrow-left.svg" alt="Назад">
      </div>
      <div class="order-title">{{ bouquetName }}</div>
      <div class="header-placeholder"></div>
    </div>
    
    <div class="photo-area">
      <div class="photo-placeholder"></div>
    </div>
    
    <div class="form-section">
      <div class="form-group">
        <div class="form-row">
          <div class="form-label">Количество цветов:</div>
          <input 
            v-model="flowerCount" 
            type="text" 
            class="form-input"
            @input="validateInput"
            @keypress="validateKeypress"
            maxlength="4"
            placeholder="Введите количество"
          />
        </div>
        <div v-if="countError" class="error-message">{{ countError }}</div>
      </div>
      
      <div class="form-group extras-group">
        <div class="extras-row">
          <div class="form-label">Допы</div>
          <div class="extras-toggle" @click="toggleExtras">
            <img src="@/assets/list-close.svg" alt="Допы">
          </div>
        </div>
      </div>
    </div>
    
    <div class="continue-button" @click="proceedToCheckout">
      <div class="price-label">Цена</div>
      <div class="continue-label">продолжить оформление</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OrderView',
  data() {
    return {
      flowerCount: '',
      countError: '',
      showExtras: false
    }
  },
  computed: {
    bouquetName() {
      return this.$route.query.bouquet || 'Название букета';
    }
  },
  mounted() {
    document.documentElement.scrollTop = 0;
    document.body.scrollTop = 0;
  },
  methods: {
    goBack() {
      this.$router.go(-1);
    },
    validateInput() {
      if (this.flowerCount === '') {
        this.countError = '';
        return;
      }
      
      const value = parseInt(this.flowerCount);
      
      if (isNaN(value)) {
        this.flowerCount = '';
        this.countError = 'Введите только цифры';
        return;
      }
      
      if (value > 5000) {
        this.flowerCount = '5000';
        this.countError = 'Максимальное количество: 5000';
      } else if (value < 1) {
        this.flowerCount = '1';
        this.countError = 'Минимальное количество: 1';
      } else {
        this.countError = '';
      }
    },
    validateKeypress(event) {
      const charCode = event.which ? event.which : event.keyCode;
      
      if (charCode < 48 || charCode > 57) {
        event.preventDefault();
        return false;
      }
      return true;
    },
    toggleExtras() {
      this.showExtras = !this.showExtras;
    },
    proceedToCheckout() {
      if (!this.flowerCount || this.countError) {
        this.countError = 'Введите корректное количество';
        return;
      }
      console.log('Переход к оформлению заказа');
    }
  }
}
</script>

<style scoped>
.order-view {
  min-height: 100vh;
  background-color: #1c1B20;
  color: white;
  padding: 20px;
  padding-top: 90px;
  padding-bottom: 150px;
  display: flex;
  flex-direction: column;
  overflow-anchor: none;
}

.order-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 40px;
  padding: 0 20px;
}

.back-button {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border-radius: 50%;
  transition: background-color 0.3s ease;
}

.back-button:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.back-button img {
  width: 24px;
  height: 24px;
  filter: brightness(0) invert(1);
}

.order-title {
  font-size: 28px;
  font-weight: 500;
  text-align: center;
  letter-spacing: 1px;
  flex: 1;
}

.header-placeholder {
  width: 40px;
}

.photo-area {
  width: calc(100% - 80px);
  max-width: 1400px;
  height: 500px;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 40px;
  margin: 0 auto 60px auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.photo-placeholder {
  width: 200px;
  height: 200px;
  background-color: rgba(255, 255, 255, 0.08);
  border-radius: 30px;
}

.form-section {
  width: calc(100% - 80px);
  max-width: 1400px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 20px;
}

.form-row {
  display: flex;
  align-items: center;
  gap: 30px;
  margin-bottom: 10px;
}

.form-label {
  font-size: 22px;
  font-weight: 500;
  color: white;
  letter-spacing: 0.5px;
  white-space: nowrap;
}

.form-input {
  width: 300px;
  height: 70px;
  background-color: rgba(255, 255, 255, 0.08);
  border: 2px solid rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  color: white;
  font-size: 20px;
  font-weight: 500;
  padding: 0 25px;
  transition: all 0.3s ease;
}

.form-input:focus {
  outline: none;
  border-color: rgba(255, 255, 255, 0.4);
  background-color: rgba(255, 255, 255, 0.12);
}

.form-input::placeholder {
  color: rgba(255, 255, 255, 0.4);
}

.error-message {
  font-size: 16px;
  color: #ff6b6b;
  margin-left: 220px;
}

.extras-group {
  margin-top: 20px;
}

.extras-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  max-width: 370px;
}

.extras-toggle {
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.08);
  transition: all 0.3s ease;
  margin-left: 20px;
}

.extras-toggle:hover {
  background-color: rgba(255, 255, 255, 0.12);
  transform: scale(1.05);
}

.extras-toggle img {
  width: 24px;
  height: 24px;
  filter: brightness(0) invert(1);
}

.continue-button {
  width: calc(100% - 80px);
  max-width: 1400px;
  height: 120px;
  background-color: rgba(255, 255, 255, 0.08);
  border-radius: 25px;
  margin: auto auto 40px auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.continue-button:hover {
  background-color: rgba(255, 255, 255, 0.12);
  transform: translateY(-5px);
}

.price-label {
  font-size: 22px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.8);
  letter-spacing: 1px;
  margin-bottom: 5px;
}

.continue-label {
  font-size: 26px;
  font-weight: 500;
  color: white;
  letter-spacing: 1px;
  text-transform: uppercase;
}

@media (max-width: 1200px) {
  .photo-area,
  .form-section,
  .continue-button {
    width: calc(100% - 60px);
  }
}

@media (max-width: 768px) {
  .order-view {
    padding-top: 80px;
    padding-bottom: 120px;
  }
  
  .order-header {
    padding: 0 15px;
    margin-bottom: 30px;
  }
  
  .order-title {
    font-size: 24px;
  }
  
  .photo-area {
    width: calc(100% - 40px);
    height: 400px;
    margin-bottom: 40px;
  }
  
  .photo-placeholder {
    width: 150px;
    height: 150px;
  }
  
  .form-section {
    width: calc(100% - 40px);
  }
  
  .form-label {
    font-size: 20px;
  }
  
  .form-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 15px;
  }
  
  .form-input {
    width: 100%;
    max-width: 300px;
    height: 60px;
    font-size: 18px;
  }
  
  .error-message {
    margin-left: 0;
  }
  
  .extras-toggle {
    width: 45px;
    height: 45px;
  }
  
  .extras-toggle img {
    width: 20px;
    height: 20px;
  }
  
  .continue-button {
    width: calc(100% - 40px);
    height: 100px;
    margin-bottom: 30px;
  }
  
  .price-label {
    font-size: 20px;
  }
  
  .continue-label {
    font-size: 22px;
  }
}

@media (max-width: 480px) {
  .order-view {
    padding-top: 76px;
    padding-left: 15px;
    padding-right: 15px;
    padding-bottom: 100px;
  }
  
  .order-header {
    padding: 0 10px;
    margin-bottom: 25px;
  }
  
  .order-title {
    font-size: 22px;
  }
  
  .back-button {
    width: 35px;
    height: 35px;
  }
  
  .back-button img {
    width: 20px;
    height: 20px;
  }
  
  .photo-area {
    width: calc(100% - 30px);
    height: 300px;
    border-radius: 30px;
    margin-bottom: 30px;
  }
  
  .photo-placeholder {
    width: 120px;
    height: 120px;
    border-radius: 20px;
  }
  
  .form-section {
    width: calc(100% - 30px);
  }
  
  .form-label {
    font-size: 18px;
  }
  
  .form-input {
    height: 55px;
    font-size: 16px;
    border-radius: 15px;
  }
  
  .error-message {
    font-size: 14px;
  }
  
  .extras-toggle {
    width: 40px;
    height: 40px;
  }
  
  .extras-toggle img {
    width: 18px;
    height: 18px;
  }
  
  .continue-button {
    width: calc(100% - 30px);
    height: 90px;
    border-radius: 20px;
    margin-bottom: 20px;
  }
  
  .price-label {
    font-size: 18px;
  }
  
  .continue-label {
    font-size: 20px;
  }
}
</style>