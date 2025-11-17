<template>
  <div class="home-view">
    <div class="hero-section">
      <div class="hero-image">
        <img src="https://images.unsplash.com/photo-1625246333195-78d9c38ad449?w=800&h=400&fit=crop" alt="Rice field" />
      </div>
      <div class="hero-text">
        Aumenta la producción aplicando los químicos correctos mediante análisis de suelo
      </div>
    </div>

    <div class="features-section">
      <h2>Características</h2>
      <div class="feature-list">
        <div class="feature-item" @click="$emit('navigate', 'field-create')">
          <div class="feature-icon">
            <i class="fas fa-cubes"></i>
          </div>
          <div class="feature-text">Crear Campo</div>
        </div>
        
        <div class="feature-item" @click="$emit('navigate', 'plantation')">
          <div class="feature-icon">
            <i class="fas fa-cubes"></i>
          </div>
          <div class="feature-text">Plantación</div>
        </div>
        
        <div class="feature-item" @click="$emit('navigate', 'soil-test')">
          <div class="feature-icon">
            <i class="fas fa-cubes"></i>
          </div>
          <div class="feature-text">Análisis de Suelo</div>
        </div>
        
        <div class="feature-item" @click="$emit('navigate', 'fertilizer')">
          <div class="feature-icon">
            <i class="fas fa-cubes"></i>
          </div>
          <div class="feature-text">Sugerencias de Plantación y Fertilizante basadas en análisis de suelo</div>
        </div>
        
        <div class="feature-item" @click="$emit('navigate', 'tracking')">
          <div class="feature-icon">
            <i class="fas fa-cubes"></i>
          </div>
          <div class="feature-text">Seguimiento de Plantación a Cosecha</div>
        </div>
        
        <div class="feature-item" @click="$emit('navigate', 'market-release')">
          <div class="feature-icon">
            <i class="fas fa-cubes"></i>
          </div>
          <div class="feature-text">Generar QR y Reporte de Liberación al Mercado</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineEmits(['navigate']);
</script>

<style scoped>
.home-view {
  padding: 0;
}

.hero-section {
  margin-bottom: 40px;
}

.hero-image {
  width: 100%;
  height: 350px;
  overflow: hidden;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.hero-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-text {
  background: white;
  padding: 20px 30px;
  font-size: 16px;
  color: #e53935;
  text-align: center;
  border-radius: 0 0 12px 12px;
  margin-top: -5px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.features-section h2 {
  color: #2c5f9d;
  font-size: 28px;
  margin-bottom: 25px;
  font-weight: 600;
}

.feature-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

.feature-item {
  background: white;
  padding: 25px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  gap: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  border-left: 4px solid transparent;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

.feature-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
  border-left-color: #4caf50;
  background: linear-gradient(135deg, #ffffff 0%, #f0f9ff 100%);
}

.feature-icon {
  width: 50px;
  height: 50px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #2c5f9d;
  font-size: 24px;
  flex-shrink: 0;
  background: transparent; /* remove blue background */
  box-shadow: none;
  border: 1px solid transparent;
  transition: all 0.18s ease;
}

.feature-item:hover .feature-icon {
  transform: scale(1.05);
  box-shadow: 0 6px 12px rgba(0,0,0,0.06);
}

.feature-text {
  flex: 1;
  font-size: 16px;
  color: #333;
  line-height: 1.5;
  font-weight: 500;
}

@media (max-width: 768px) {
  .hero-image {
    height: 250px;
  }

  .feature-list {
    grid-template-columns: 1fr;
  }

  .features-section h2 {
    font-size: 24px;
  }
}
</style>
