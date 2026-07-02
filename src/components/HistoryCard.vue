<template>
  <div class="record-card">
    <div class="card-header">
      <span class="record-date">📅 Calculated on: {{ record.date }}</span>
      <button @click="$emit('delete-record', index)" class="btn-clear-single">Delete</button>
    </div>
    <div class="card-body">
      <div class="stat">
        <span class="label">Total Semesters Included:</span>
        <span class="value">{{ record.semestersCount }}</span>
      </div>
      <div class="stat score-row">
        <span class="label">Calculated Cumulative Score:</span>
        <span class="value score">{{ record.cgpa }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  record: Object,
  index: Number
})
defineEmits(['delete-record'])
</script>

<style scoped>
.record-card {
  background: white;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.03);
  border-left: 5px solid #27ae60;
}
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
  border-bottom: 1px solid #f1f2f6;
  padding-bottom: 8px;
}
.record-date {
  font-size: 13px;
  color: #95a5a6;
}
.btn-clear-single {
  background: none;
  color: #e74c3c;
  border: 1px solid #e74c3c;
  padding: 4px 10px;
  font-size: 12px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.2s;
}
.btn-clear-single:hover {
  background: #e74c3c;
  color: white;
}
.stat {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
  font-size: 14px;
  color: #57606f;
}
.score-row {
  border-top: 1px dashed #f1f2f6;
  padding-top: 10px;
  margin-top: 10px;
}
.score {
  font-size: 22px;
  font-weight: bold;
  color: #27ae60;
}
</style>