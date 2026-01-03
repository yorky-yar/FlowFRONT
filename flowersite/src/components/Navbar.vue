<template>
    <nav class="navbar-top" :class="{ 'navbar-hidden': isHidden, 'navbar-scrolled': isScrolled }">
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
    </nav>
</template>

<script>
export default {
    name: "NavbarTop",
    data() {
        return {
            isMenuOpen: false,
            isHidden: false,
            isScrolled: false,
            lastScrollPosition: 0,
            scrollTimeout: null
        }
    },
    mounted() {
        document.addEventListener('keydown', this.handleEscape);
        window.addEventListener('scroll', this.handleScroll);
    },
    beforeUnmount() {
        document.removeEventListener('keydown', this.handleEscape);
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        toggleMenu() {
            this.isMenuOpen = !this.isMenuOpen;
            if (this.isMenuOpen) {
                document.body.style.overflow = 'hidden';
            } else {
                document.body.style.overflow = '';
            }
        },
        closeMenu() {
            this.isMenuOpen = false;
            document.body.style.overflow = '';
        },
        handleEscape(e) {
            if (e.key === 'Escape' && this.isMenuOpen) {
                this.closeMenu();
            }
        },
        navigateTo(route) {
            this.closeMenu();
            if (this.$route.name !== route) {
                this.$router.push({ name: route });
            }
        },
        handleScroll() {
            const currentScrollPosition = window.pageYOffset || document.documentElement.scrollTop;
            
            if (currentScrollPosition < 50) {
                this.isHidden = false;
                this.isScrolled = false;
                return;
            }
            
            this.isScrolled = true;
            
            if (Math.abs(currentScrollPosition - this.lastScrollPosition) < 60) {
                return;
            }
            
            if (currentScrollPosition > this.lastScrollPosition && currentScrollPosition > 100) {
                this.isHidden = true;
            } else {
                this.isHidden = false;
            }
            
            this.lastScrollPosition = currentScrollPosition;
        }
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
    transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1), background-color 0.3s ease;
    transform: translateY(0);
}

.navbar-top::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 0.5px;
    background-color: rgba(255, 255, 255, 0.267);
    transition: opacity 0.3s ease;
}

.navbar-top.navbar-hidden {
    transform: translateY(-100%);
}

.navbar-top.navbar-scrolled {
    background-color: rgba(28, 27, 32, 0.95);
    backdrop-filter: blur(10px);
}

.navbar-top.navbar-scrolled::after {
    opacity: 0.3;
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
    cursor: pointer;
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
}

@media (min-width: 1200px) {
    .navbar-top-container {
        max-width: 1200px;
    }
}
</style>