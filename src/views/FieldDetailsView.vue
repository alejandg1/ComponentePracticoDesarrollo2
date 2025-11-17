<template>
  <div class="field-details-view">
    <div class="detail-section">
      <div class="detail-row">
        <span class="detail-label">Field</span>
        <span class="detail-value">{{ data.fieldAmount }}</span>
      </div>
      
      <div class="detail-row">
        <span class="detail-label">Amount</span>
        <span class="detail-value">{{ data.fieldAmount }}</span>
      </div>
      
      <div class="detail-row">
        <span class="detail-label">Field Type</span>
        <span class="detail-value">{{ data.fieldType }}</span>
      </div>
      
      <div class="detail-row">
        <span class="detail-label">Crop Name</span>
        <span class="detail-value">{{ data.cropName }}</span>
      </div>
    </div>
    
    <div class="detail-section">
      <div class="detail-row">
        <span class="detail-label">Soil Report</span>
        <span class="detail-value">{{ data.soilReport.date }}</span>
        <span class="detail-value values">
          n: {{ data.soilReport.n }}<br>
          p: {{ data.soilReport.p }}<br>
          k: {{ data.soilReport.k }}
        </span>
      </div>
    </div>
    
    <div class="detail-section">
      <div class="detail-row">
        <span class="detail-label">Fertilizer</span>
        <span class="detail-value">{{ data.fertilizer.date }}</span>
        <span class="detail-value values">
          Urea: {{ data.fertilizer.urea }}<br>
          Potassium Sulphate: {{ data.fertilizer.potassium }}
        </span>
      </div>
    </div>
    
    <div class="detail-section">
      <div class="detail-row">
        <span class="detail-label">Crop Plantation Date</span>
        <span class="detail-value highlight">{{ data.cropPlantationDate }}</span>
      </div>
      
      <div class="detail-row">
        <span class="detail-label">Crop Harvesting Date</span>
        <span class="detail-value highlight">{{ data.cropHarvestingDate }}</span>
      </div>
      
      <div class="detail-row">
        <span class="detail-label">Market Released Date</span>
        <span class="detail-value highlight">{{ data.marketReleasedDate }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  fieldData: {
    type: Object,
    default: () => null
  }
});

const data = computed(() => {
  return props.fieldData || {
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
  };
});
</script>

<style scoped>
.field-details-view {
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
  background: #f5f5f5;
  min-height: calc(100vh - 160px);
}

.detail-section {
  background: white;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 15px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.detail-row {
  display: grid;
  grid-template-columns: 140px 1fr;
  padding: 12px 0;
  gap: 10px;
  align-items: start;
}

.detail-label {
  font-size: 14px;
  color: #999;
  font-weight: 400;
}

.detail-value {
  font-size: 14px;
  color: #333;
  font-weight: 500;
}

.detail-value.values {
  line-height: 1.6;
  color: #333;
}

.detail-value.highlight {
  color: #2c5f9d;
  font-weight: 600;
}

@media (max-width: 768px) {
  .field-details-view {
    padding: 15px;
  }
  
  .detail-section {
    padding: 15px;
  }
  
  .detail-row {
    grid-template-columns: 1fr;
    gap: 5px;
  }
}
</style>
