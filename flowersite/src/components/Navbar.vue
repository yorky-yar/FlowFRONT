<template>
    <nav class="navbar-top">
        <div class="navbar-top-container">
            <div class="left-section">
                <div class="profile-circle">
                    <div class="profile-placeholder"></div>
                </div>
            </div>
            
            <div class="center-section">
                <div class="company-name">SILKBUDS</div>
            </div>
            
            <div class="right-section">
                <div class="menu-icon">
                    <img src="@/assets/menu.svg" alt="Menu">
                </div>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    name: "NavbarTop",
    data() {
        return {}
    }
}
</script>

<style scoped>
.navbar-top {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: 70px;
    background-color: transparent;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    margin: 0;
    max-width: 100%;
    padding-top: env(safe-area-inset-top, 0px);
}

.navbar-top::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 0.5px;
    background-color: rgba(255, 255, 255, 0.267);
}

.navbar-top-container {
    display: flex;
    align-items: center;
    width: 100%;
    max-width: 1200px;
    height: 100%;
    position: relative;
    margin: 0 auto;
    padding: 0 20px;
}

.left-section {
    flex: 1;
    display: flex;
    justify-content: flex-start;
}

.center-section {
    flex: 1;
    display: flex;
    justify-content: center;
}

.right-section {
    flex: 1;
    display: flex;
    justify-content: flex-end;
}

.profile-circle {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.profile-placeholder {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background-color: #1c1B20;
}

.company-name {
    font-size: 24px;
    font-weight: 500;
    color: white;
    text-align: center;
    letter-spacing: 0.5px;
}

.menu-icon {
    width: 60px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.menu-icon img {
    width: 30px;
    height: 30px;
    object-fit: contain;
}

@media (max-width: 768px) {
    .navbar-top {
        height: 60px;
    }
    
    .company-name {
        font-size: 20px;
    }
    
    .profile-circle {
        width: 36px;
        height: 36px;
    }
    
    .profile-placeholder {
        width: 32px;
        height: 32px;
    }
    
    .menu-icon img {
        width: 28px;
        height: 28px;
    }
}

@media (max-width: 480px) {
    .navbar-top {
        height: 56px;
    }
    
    .company-name {
        font-size: 18px;
    }
    
    .profile-circle {
        width: 32px;
        height: 32px;
    }
    
    .profile-placeholder {
        width: 28px;
        height: 28px;
    }
    
    .menu-icon img {
        width: 25px;
        height: 25px;
    }
}

@media (min-width: 1200px) {
    .navbar-top-container {
        max-width: 1200px;
    }
}
</style>