<template>
  <div class="soil-test-view">
    <h2>Add soil test information</h2>
    
    <form @submit.prevent="handleSubmit" class="test-form">
      <div class="form-group">
        <label>Field</label>
        <select v-model="form.field" class="form-control">
          <option value="F1">F1</option>
          <option value="F2">F2</option>
          <option value="F3">F3</option>
        </select>
      </div>
      
      <div class="form-group">
        <label>Soild Report</label>
        <input 
          type="text" 
          v-model="form.soilReport" 
          class="form-control"
          placeholder="50"
        />
      </div>
      
      <div class="form-group">
        <input 
          type="text" 
          v-model="form.value1" 
          class="form-control"
          placeholder="10"
        />
      </div>
      
      <div class="form-group">
        <input 
          type="text" 
          v-model="form.value2" 
          class="form-control"
          placeholder="12"
        />
      </div>
      
      <div class="form-actions">
        <button type="submit" class="btn btn-primary">Submit</button>
        <button type="button" @click="resetForm" class="btn btn-secondary">Reset</button>
      </div>
    </form>
    
    <div class="soil-test-list">
      <h3>Soil Test List</h3>
      <div class="table-container">
        <table class="test-table">
          <thead>
            <tr>
              <th>Field Name</th>
              <th>Soil Test Report</th>
              <th>Create At</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(test, index) in tests" :key="index">
              <td>{{ test.fieldName }}</td>
              <td>{{ test.soilReport }}</td>
              <td>{{ test.createAt }}</td>
              <td>
                <button 
                  class="btn-action" 
                  @click="$emit('navigate', 'field-details', test)"
                >
                  View
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['navigate']);

const form = ref({
  field: 'F1',
  soilReport: '50',
  value1: '10',
  value2: '12'
});

const tests = ref([
  { fieldName: 'F1', soilReport: '50', createAt: '2023-06-15' },
  { fieldName: 'F2', soilReport: '45', createAt: '2023-06-14' }
]);

const handleSubmit = () => {
  tests.value.push({
    fieldName: form.value.field,
    soilReport: form.value.soilReport,
    createAt: new Date().toISOString().split('T')[0]
  });
  resetForm();
};

const resetForm = () => {
  form.value = {
    field: 'F1',
    soilReport: '50',
    value1: '10',
    value2: '12'
  };
};
</script>

<style scoped>
.soil-test-view {
  padding: 0;
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
  margin-bottom: 20px;
  font-weight: 600;
}

.test-form {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 40px;
  max-width: 700px;
  margin: 0 auto; /* center the form */
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
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 15px;
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
  min-width: 120px;
}

.btn-primary {
  background: linear-gradient(135deg, #2c5f9d 0%, #1e4578 100%);
  color: white;
  box-shadow: 0 4px 12px rgba(44, 95, 157, 0.3);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(44, 95, 157, 0.4);
}

.btn-secondary {
  background: #e9ecef;
  color: #495057;
}

.btn-secondary:hover {
  background: #dee2e6;
  transform: translateY(-2px);
}

.soil-test-list {
  margin-top: 40px;
}

.table-container {
  overflow-x: auto;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.test-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 15px;
}

.test-table thead {
  background: linear-gradient(135deg, #2c5f9d 0%, #1e4578 100%);
  color: white;
}

.test-table th {
  padding: 16px 20px;
  text-align: left;
  font-weight: 600;
}

.test-table td {
  padding: 16px 20px;
  border-bottom: 1px solid #e9ecef;
  color: #212529;
}

.test-table tbody tr:hover {
  background: #f8f9fa;
}

.test-table tbody tr:last-child td {
  border-bottom: none;
}

.btn-action {
  background: linear-gradient(135deg, #2c5f9d 0%, #1e4578 100%);
  color: white;
  border: none;
  padding: 8px 20px;
  border-radius: 6px;
  font-size: 14px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s;
}

.btn-action:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(44, 95, 157, 0.3);
}

@media (max-width: 768px) {
  h2 {
    font-size: 24px;
  }

  .test-form {
    padding: 20px;
  }

  .form-actions {
    flex-direction: column;
  }

  .btn {
    width: 100%;
  }
}
</style>
