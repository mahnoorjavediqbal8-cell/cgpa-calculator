<template>
  <div class="history-container">
    <div class="header-section">
      <h2>📜 Saved Academic Records</h2>
      <p>Tracking dashboard configuration records matrix.</p>
    </div>

    <div v-if="records.length === 0" class="empty-state">
      <div class="empty-icon">📂</div>
      <h3>No Records Present</h3>
      <button @click="$router.push('/')" class="btn-redirect">Return to Engine</button>
    </div>

    <div v-else class="records-grid">
      <HistoryCard 
        v-for="(record, index) in records" 
        :key="record.id"
        :record="record"
        :index="index"
        @delete-record="purgeRecord"
      />
      <div class="global-actions">
        <button @click="purgeAll" class="btn-danger-all">Wipe History Logs</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import HistoryCard from '../components/HistoryCard.vue'

const records = ref([])

onMounted(() => {
  records.value = JSON.parse(localStorage.getItem('academic_history') || '[]')
})

const purgeRecord = (index) => {
  records.value.splice(index, 1)
  localStorage.setItem('academic_history', JSON.stringify(records.value))
}

const purgeAll = () => {
  if (confirm("Execute global data factory reset?")) {
    records.value = []
    localStorage.removeItem('academic_history')
  }
}
</script>

<style scoped>
.history-container { max-width: 650px; margin: 0 auto; }
.header-section { text-align: center; margin-bottom: 25px; }
.empty-state { background: white; border-radius: 12px; padding: 40px; text-align: center; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
.empty-icon { font-size: 48px; margin-bottom: 10px; }
.btn-redirect { background-color: #d35400; color: white; margin-top: 15px; padding: 10px 20px; border-radius: 6px; border: none; cursor: pointer; font-weight: bold;}
.records-grid { display: flex; flex-direction: column; gap: 15px; }
.global-actions { text-align: center; margin-top: 20px; }
.btn-danger-all { background-color: #e74c3c; color: white; padding: 11px 22px; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;}
</style>