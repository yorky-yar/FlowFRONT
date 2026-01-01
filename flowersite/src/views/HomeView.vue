<template>
  <div class="home">
    <div class="top-rectangle">
      <div class="rectangle-label">КЛАССИЧЕСКИЙ</div>
      <div class="small-rectangle">
        <div class="small-rectangle-label">ЗАКАЗАТЬ</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView'
}
</script>

<style scoped>
.home {
  min-height: 100vh;
  color: white;
  padding: 20px;
  padding-top: 90px;
}

.top-rectangle {
  width: calc(100% - 200px);
  height: 500px;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 100px;
  margin:  auto;
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
}

.small-rectangle-label {
  font-size: 25px;
  font-weight: 400;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
}

@media (max-width: 768px) {
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
}

@media (max-width: 480px) {
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
}
</style>