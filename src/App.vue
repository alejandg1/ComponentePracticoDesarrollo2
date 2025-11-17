<script setup>
import { ref } from 'vue';
import HomeView from './views/HomeView.vue';
import SoilTestView from './views/SoilTestView.vue';
import MarketReleaseView from './views/MarketReleaseView.vue';
import FieldDetailsView from './views/FieldDetailsView.vue';

const currentView = ref('home');
const viewHistory = ref(['home']);
const selectedData = ref(null);



const navigate = (view, data = null) => {
  currentView.value = view;
  selectedData.value = data;
  viewHistory.value.push(view);
};

const goBack = () => {
  if (viewHistory.value.length > 1) {
    viewHistory.value.pop();
    currentView.value = viewHistory.value[viewHistory.value.length - 1];
  } else {
    currentView.value = 'home';
    viewHistory.value = ['home'];
  }
  // clear selected data when navigating back to avoid stale context
  selectedData.value = null;
};

const goHome = () => {
  currentView.value = 'home';
  viewHistory.value = ['home'];
  selectedData.value = null;
};
</script>

<template>
  <div class="app-wrapper">
    <!-- Header -->
    <header class="app-header">
      <div class="header-content">
        <nav class="main-nav">
          <button 
            :class="['nav-link', { active: currentView === 'home' }]" 
            @click="goHome"
          >
            <i class="fas fa-home"></i>
            Home
          </button>
          <button 
            :class="['nav-link', { active: currentView === 'soil-test' }]" 
            @click="navigate('soil-test')"
          >
            <i class="fas fa-flask"></i>
            Soil Test
          </button>
          <button 
            :class="['nav-link', { active: currentView === 'market-release' }]" 
            @click="navigate('market-release')"
          >
            <i class="fas fa-qrcode"></i>
            Market Release
          </button>
        </nav>
        <div class="header-actions">
          <button class="btn-icon" @click="goBack" title="Go Back">
            <i class="fas fa-arrow-left"></i>
          </button>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="app-main">
      <Transition name="fade" mode="out-in">
        <HomeView 
          v-if="currentView === 'home'" 
          @navigate="navigate"
        />
        <SoilTestView 
          v-else-if="currentView === 'soil-test'" 
          @navigate="navigate"
        />
        <MarketReleaseView 
          v-else-if="currentView === 'market-release'" 
          @navigate="navigate"
        />
        <FieldDetailsView 
          v-else-if="currentView === 'field-details'" 
          :field-data="selectedData"
        />
        <div v-else class="placeholder-view">
          <h2>{{ currentView }}</h2>
          <p>Feature coming soon...</p>
        </div>
      </Transition>
    </main>

    
  </div>
</template>

<style scoped>
.app-wrapper {
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: #f5f7fa;
}

/* Header */
.app-header {
  background: linear-gradient(135deg, #2c5f9d 0%, #1e4578 100%);
  color: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 100;
}

.header-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 30px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 70px;
  gap: 30px;
}

/* logo styles removed (logo markup was deleted) */

.main-nav {
  display: flex;
  gap: 10px;
  flex: 1;
  justify-content: center;
}

.nav-link {
  background: rgba(255, 255, 255, 0.1);
  border: none;
  color: white;
  padding: 10px 20px;
  border-radius: 8px;
  font-size: 15px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  display: flex;
  align-items: center;
  gap: 8px;
}

.nav-link i {
  font-size: 14px;
}

.nav-link:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
}

.nav-link.active {
  background: rgba(255, 255, 255, 0.25);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 15px;
}

.btn-icon {
  background: rgba(255, 255, 255, 0.1);
  border: none;
  color: white;
  width: 40px;
  height: 40px;
  border-radius: 8px;
  font-size: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn-icon:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
}

.time { /* removed - clock UI deleted */ }
.time i { /* removed */ }

/* Main Content */
.app-main {
  flex: 1;
  max-width: 1400px;
  width: 100%;
  margin: 0 auto;
  padding: 30px;
  overflow-y: auto;
}

/* Footer styles removed (footer element deleted) */

.placeholder-view {
  padding: 60px 20px;
  text-align: center;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.placeholder-view h2 {
  color: #2c5f9d;
  margin-bottom: 10px;
  text-transform: capitalize;
  font-size: 32px;
}

.placeholder-view p {
  color: #666;
  font-size: 18px;
}

/* Transitions */
.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

/* Responsive */
@media (max-width: 768px) {
  .header-content {
    padding: 0 15px;
    height: auto;
    flex-wrap: wrap;
    padding-top: 15px;
    padding-bottom: 15px;
  }

  .logo h1 {
    font-size: 18px;
  }

  .main-nav {
    order: 3;
    width: 100%;
    justify-content: flex-start;
    overflow-x: auto;
    padding-top: 10px;
  }

  .nav-link {
    padding: 8px 16px;
    font-size: 14px;
  }

  .app-main {
    padding: 20px 15px;
  }
}
</style>
