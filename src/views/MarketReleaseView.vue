<template>
  <div class="market-release-view">
    <h2>Market Release information</h2>
    
    <form @submit.prevent="handleSubmit" class="release-form">
      <div class="form-group">
        <label>Field</label>
        <select v-model="form.field" class="form-control">
          <option value="">Choose Field...</option>
          <option value="F1">F1</option>
          <option value="F2">F2</option>
          <option value="F3">F3</option>
        </select>
      </div>
      
      <div class="form-group">
        <label>Crop Name</label>
        <input 
          type="text" 
          v-model="form.cropName" 
          class="form-control"
          placeholder="Enter crop name"
        />
      </div>
      
      <div class="form-actions">
        <button type="submit" class="btn btn-primary">Submit</button>
        <button type="button" @click="resetForm" class="btn btn-secondary">Reset</button>
      </div>
    </form>
    
    <div class="market-history">
      <h3>Market Released History</h3>
      
      <div class="qr-cards">
        <div v-for="(release, index) in releases" :key="index" class="qr-card">
          <div class="qr-header">
            <span class="qr-label">Field Name</span>
            <span class="qr-code-label">QR</span>
          </div>
          <div class="qr-content">
            <div class="field-name">{{ release.fieldName }}</div>
            <div class="qr-code-container">
              <div class="qr-code">
                <svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                  <rect width="100" height="100" fill="white"/>
                  <rect x="10" y="10" width="25" height="25" fill="black"/>
                  <rect x="65" y="10" width="25" height="25" fill="black"/>
                  <rect x="10" y="65" width="25" height="25" fill="black"/>
                  <rect x="15" y="15" width="15" height="15" fill="white"/>
                  <rect x="70" y="15" width="15" height="15" fill="white"/>
                  <rect x="15" y="70" width="15" height="15" fill="white"/>
                  <rect x="45" y="20" width="5" height="5" fill="black"/>
                  <rect x="55" y="20" width="5" height="5" fill="black"/>
                  <rect x="45" y="45" width="5" height="5" fill="black"/>
                  <rect x="55" y="45" width="5" height="5" fill="black"/>
                  <rect x="45" y="70" width="5" height="5" fill="black"/>
                  <rect x="65" y="45" width="5" height="5" fill="black"/>
                  <rect x="75" y="55" width="5" height="5" fill="black"/>
                </svg>
              </div>
              <a href="#" class="view-link" @click.prevent="$emit('navigate', 'field-details', release)">
                View
              </a>
            </div>
          </div>
        </div>
      </div>
      
      
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['navigate']);

const form = ref({
  field: '',
  cropName: ''
});

const releases = ref([
  { 
    fieldName: 'F1', 
    qrCode: 'QR123',
    fieldAmount: '2',
    fieldType: 'Loamy Soil',
    cropName: 'Rice',
    soilReport: {
      date: 'On: 15 Jun, 2023',
      n: '50',
      p: '10',
      k: '12'
    },
    fertilizer: {
      date: 'On: 15 Jun, 2023',
      urea: '10kg',
      potassium: '5kg'
    },
    cropPlantationDate: 'Thu, 15 Jun, 2023 3:34 am UT',
    cropHarvestingDate: 'Thu, 15 Jun, 2023 3:37 am UT',
    marketReleasedDate: 'Thu, 15 Jun, 2023 3:37 am UT'
  }
]);

const handleSubmit = () => {
  if (form.value.field && form.value.cropName) {
    releases.value.push({
      fieldName: form.value.field,
      qrCode: `QR${Date.now()}`,
      fieldAmount: '2',
      fieldType: 'Loamy Soil',
      cropName: form.value.cropName,
      soilReport: {
        date: 'On: 15 Jun, 2023',
        n: '50',
        p: '10',
        k: '12'
      },
      fertilizer: {
        date: 'On: 15 Jun, 2023',
        urea: '10kg',
        potassium: '5kg'
      },
      cropPlantationDate: 'Thu, 15 Jun, 2023 3:34 am UT',
      cropHarvestingDate: 'Thu, 15 Jun, 2023 3:37 am UT',
      marketReleasedDate: 'Thu, 15 Jun, 2023 3:37 am UT'
    });
    resetForm();
  }
};

const resetForm = () => {
  form.value = {
    field: '',
    cropName: ''
  };
};
</script>

<style scoped>
.market-release-view {
  padding: 40px 20px;
  max-width: 1400px;
  margin: 0 auto;
}

h2 {
  color: #2c5f9d;
  font-size: 32px;
  margin-bottom: 30px;
  font-weight: 600;
}

h3 {
  color: #2c5f9d;
  font-size: 24px;
  margin-bottom: 25px;
  font-weight: 600;
}

.release-form {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 40px;
  max-width: 800px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  color: #495057;
  font-size: 15px;
  margin-bottom: 8px;
  font-weight: 500;
}

.form-control {
  width: 100%;
  padding: 14px 16px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 16px;
  background: white;
  transition: all 0.3s;
}

.form-control:focus {
  outline: none;
  border-color: #2c5f9d;
  box-shadow: 0 0 0 3px rgba(44, 95, 157, 0.1);
}

.form-actions {
  display: flex;
  gap: 15px;
  margin-top: 25px;
}

.btn {
  padding: 14px 32px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
  flex: 1;
}

.btn-primary {
  background: linear-gradient(135deg, #2c5f9d 0%, #1e4578 100%);
  color: white;
  box-shadow: 0 4px 6px rgba(44, 95, 157, 0.2);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(44, 95, 157, 0.3);
}

.btn-primary:active {
  transform: translateY(0);
}

.btn-secondary {
  background: #e9ecef;
  color: #495057;
}

.btn-secondary:hover {
  background: #dee2e6;
}

.btn-secondary:active {
  transform: scale(0.98);
}

.market-history {
  margin-top: 40px;
}

.qr-cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 25px;
}

.qr-card {
  background: white;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: all 0.3s;
}

.qr-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

.qr-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  font-size: 14px;
  color: #666;
}

.qr-content {
  display: flex;
  align-items: center;
  gap: 25px;
}

.field-name {
  font-size: 22px;
  font-weight: 600;
  color: #333;
  flex: 1;
}

.qr-code-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.qr-code {
  width: 200px;
  height: 200px;
  background: white;
  border: 2px solid #ddd;
  border-radius: 12px;
  padding: 15px;
}

.qr-code svg {
  width: 100%;
  height: 100%;
}

.view-link {
  color: #2c5f9d;
  text-decoration: none;
  font-size: 15px;
  font-weight: 600;
  transition: color 0.3s;
}

.view-link:hover {
  color: #1e4578;
  text-decoration: underline;
}

.view-link:active {
  color: #4c6ef5;
}


@media (max-width: 768px) {
  .market-release-view {
    padding: 20px 15px;
  }
  
  h2 {
    font-size: 24px;
  }
  
  h3 {
    font-size: 20px;
  }
  
  .release-form {
    padding: 20px;
  }
  
  .form-actions {
    flex-direction: column;
  }
  
  .qr-cards {
    grid-template-columns: 1fr;
  }
  
  .qr-content {
    flex-direction: column;
    text-align: center;
  }
  
  .qr-code {
    width: 150px;
    height: 150px;
  }
}
</style>
