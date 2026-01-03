<template>
  <div class="home">
    <div class="top-rectangle">
      <div class="rectangle-label">КЛАССИЧЕСКИЙ</div>
      <div class="small-rectangle" @click="goToOrder('КЛАССИЧЕСКИЙ')">
        <div class="small-rectangle-label">ЗАКАЗАТЬ</div>
      </div>
    </div>
    
    <div class="divider-line"></div>
    
    <div class="section-title">Дизайнерские букеты</div>
    
    <div class="designer-section">
      <div class="designer-bouquet">
        <div class="bouquet-name">РОМАНТИКА</div>
        <div class="bouquet-description">Описание букета</div>
        <div class="small-rectangle" @click="goToOrder('РОМАНТИКА')">
          <div class="small-rectangle-label">ЗАКАЗАТЬ</div>
        </div>
      </div>
      
      <div class="designer-bouquet">
        <div class="bouquet-name">МИНИМАЛИЗМ</div>
        <div class="bouquet-description">Описание букета</div>
        <div class="small-rectangle" @click="goToOrder('МИНИМАЛИЗМ')">
          <div class="small-rectangle-label">ЗАКАЗАТЬ</div>
        </div>
      </div>
      
      <div class="designer-bouquet">
        <div class="bouquet-name">ПРЕМИУМ</div>
        <div class="bouquet-description">Описание букета</div>
        <div class="small-rectangle" @click="goToOrder('ПРЕМИУМ')">
          <div class="small-rectangle-label">ЗАКАЗАТЬ</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView',
  mounted() {
    document.documentElement.scrollTop = 0;
    document.body.scrollTop = 0;
  },
  methods: {
    goToOrder(bouquetName) {
      this.$router.push({ 
        name: 'order',
        query: { bouquet: bouquetName }
      });
    }
  }
}
</script>

<style scoped>
.home {
  min-height: 100vh;
  color: white;
  padding: 20px;
  padding-top: 90px;
  overflow-anchor: none;
}

.top-rectangle {
  width: calc(100% - 200px);
  height: 500px;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 100px;
  margin: auto;
  margin-top: 20px;
  position: relative;
}

.rectangle-label {
  position: absolute;
  top: 70px;
  left: 80px;
  font-size: 35px;
  font-weight: 500;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.small-rectangle {
  position: absolute;
  bottom: 50px;
  left: 80px;
  width: 300px;
  height: 100px;
  background-color: rgba(255, 255, 255, 0.08);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.small-rectangle:hover {
  background-color: rgba(255, 255, 255, 0.12);
  transform: translateY(-3px);
}

.small-rectangle-label {
  font-size: 25px;
  font-weight: 400;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.divider-line {
  width: calc(100% - 200px);
  height: 1px;
  background-color: rgba(255, 255, 255, 0.1);
  margin: 80px auto 60px auto;
}

.section-title {
  width: calc(100% - 200px);
  margin: 0 auto 60px auto;
  font-size: 35px;
  font-weight: 500;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.designer-section {
  width: calc(100% - 200px);
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 80px;
}

.designer-bouquet {
  width: 100%;
  height: 500px;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 100px;
  position: relative;
  padding: 70px 80px 0 80px;
}

.bouquet-name {
  font-size: 35px;
  font-weight: 500;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 30px;
}

.bouquet-description {
  font-size: 20px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  margin-bottom: 50px;
  max-width: 600px;
}

.designer-bouquet .small-rectangle {
  position: static;
  width: 300px;
  height: 100px;
  background-color: rgba(255, 255, 255, 0.08);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.designer-bouquet .small-rectangle:hover {
  background-color: rgba(255, 255, 255, 0.12);
  transform: translateY(-3px);
}

@media (max-width: 1200px) {
  .top-rectangle,
  .divider-line,
  .section-title,
  .designer-section {
    width: calc(100% - 100px);
  }
}

@media (max-width: 992px) {
  .top-rectangle,
  .divider-line,
  .section-title,
  .designer-section {
    width: calc(100% - 60px);
  }
  
  .designer-bouquet {
    padding: 50px 60px 0 60px;
  }
}

@media (max-width: 768px) {
  .home {
    padding-top: 80px;
  }
  
  .top-rectangle {
    width: calc(100% - 40px);
    height: 250px;
    border-radius: 60px;
  }
  
  .rectangle-label {
    font-size: 24px;
    top: 40px;
    left: 40px;
  }
  
  .small-rectangle {
    bottom: 20px;
    left: 40px;
    width: 200px;
    height: 80px;
    border-radius: 20px;
  }
  
  .small-rectangle-label {
    font-size: 20px;
  }
  
  .divider-line {
    width: calc(100% - 40px);
    margin: 60px auto 40px auto;
  }
  
  .section-title {
    width: calc(100% - 40px);
    font-size: 24px;
    margin-bottom: 40px;
  }
  
  .designer-section {
    width: calc(100% - 40px);
    gap: 60px;
  }
  
  .designer-bouquet {
    height: 400px;
    border-radius: 60px;
    padding: 40px 40px 0 40px;
  }
  
  .bouquet-name {
    font-size: 24px;
    margin-bottom: 20px;
  }
  
  .bouquet-description {
    font-size: 18px;
    margin-bottom: 40px;
  }
  
  .designer-bouquet .small-rectangle {
    width: 200px;
    height: 80px;
  }
}

@media (max-width: 576px) {
  .designer-bouquet {
    height: 350px;
    padding: 30px 30px 0 30px;
  }
  
  .bouquet-description {
    font-size: 16px;
    margin-bottom: 30px;
  }
  
  .designer-bouquet .small-rectangle {
    width: 180px;
    height: 70px;
  }
  
  .small-rectangle-label {
    font-size: 18px;
  }
}

@media (max-width: 480px) {
  .home {
    padding-top: 76px;
  }
  
  .top-rectangle {
    width: calc(100% - 40px);
    height: 200px;
    border-radius: 40px;
  }
  
  .rectangle-label {
    font-size: 20px;
    top: 25px;
    left: 25px;
  }
  
  .small-rectangle {
    bottom: 15px;
    left: 25px;
    width: 150px;
    height: 60px;
    border-radius: 15px;
  }
  
  .small-rectangle-label {
    font-size: 16px;
  }
  
  .divider-line {
    margin: 40px auto 30px auto;
  }
  
  .section-title {
    font-size: 20px;
    margin-bottom: 30px;
  }
  
  .designer-section {
    gap: 40px;
  }
  
  .designer-bouquet {
    height: 300px;
    border-radius: 40px;
    padding: 25px 25px 0 25px;
  }
  
  .bouquet-name {
    font-size: 20px;
    margin-bottom: 15px;
  }
  
  .bouquet-description {
    font-size: 15px;
    margin-bottom: 25px;
  }
  
  .designer-bouquet .small-rectangle {
    width: 150px;
    height: 60px;
  }
}
</style>