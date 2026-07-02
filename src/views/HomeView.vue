<template>
  <div class="dashboard-container">
    <div class="header-section">
      <h2>📊 Academic CGPA Dashboard</h2>
      <p>Configure semesters to compute final grade point statistics.</p>
    </div>

    <div class="calculator-card">
      <SemesterTable 
        v-for="(semester, index) in semesters" 
        :key="index"
        :semester="semester"
        :index="index"
        @update-data="mutateSemesterData"
        @remove-semester="removeSemester"
      />

      <div class="control-buttons">
        <button @click="addSemester" class="btn-secondary" type="button">➕ Add Semester</button>
        <button @click="executeCalculation" class="btn-primary" type="button">🔢 Calculate CGPA</button>
      </div>

      <div v-if="cgpa !== null" class="result-display">
        <p>Cumulative GPA (CGPA)</p>
        <div class="cgpa-value">{{ cgpa }}</div>
        <button @click="persistRecord" class="btn-save" type="button">💾 Save Locally</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import SemesterTable from '../components/SemesterTable.vue'

const semesters = ref([{ gpa: '', credits: '' }])
const cgpa = ref(null)

const addSemester = () => {
  semesters.value.push({ gpa: '', credits: '' })
}

const removeSemester = (index) => {
  if (semesters.value.length > 1) {
    semesters.value.splice(index, 1)
  }
}

// Handler catching input payload from Child Component Emits
const mutateSemesterData = (index, field, value) => {
  if (value === '') {
    semesters.value[index][field] = ''
  } else {
    semesters.value[index][field] = field === 'gpa' ? parseFloat(value) : parseInt(value)
  }
}

const executeCalculation = () => {
  let accumulatedPoints = 0
  let accumulatedCredits = 0

  semesters.value.forEach(sem => {
    if (sem.gpa !== '' && sem.credits !== '') {
      accumulatedPoints += (sem.gpa * sem.credits)
      accumulatedCredits += sem.credits
    }
  })

  if (accumulatedCredits > 0) {
    cgpa.value = (accumulatedPoints / accumulatedCredits).toFixed(2)
  } else {
    alert("Incomplete data fields. Processing aborted.")
  }
}

const persistRecord = () => {
  if (cgpa.value === null) return
  const dataPayload = JSON.parse(localStorage.getItem('academic_history') || '[]')
  dataPayload.push({
    id: Date.now(),
    date: new Date().toLocaleDateString(),
    cgpa: cgpa.value,
    semestersCount: semesters.value.length
  })
  localStorage.setItem('academic_history', JSON.stringify(dataPayload))
  alert("Calculation state persistent on system storage.")
}
</script>

<style scoped>
.dashboard-container { max-width: 650px; margin: 0 auto; }
.header-section { text-align: center; margin-bottom: 25px; }
.calculator-card { background: white; border-radius: 12px; padding: 30px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
.control-buttons { display: flex; gap: 15px; margin-top: 25px; justify-content: center; }
button { padding: 11px 22px; border: none; border-radius: 6px; font-weight: 600; cursor: pointer; }
.btn-primary { background-color: #d35400; color: white; }
.btn-primary:hover { background-color: #b34500; }
.btn-secondary { background-color: #ecf0f1; color: #2c3e50; }
.btn-secondary:hover { background-color: #bdc3c7; }
.result-display { margin-top: 30px; background: #e8f8f5; border: 2px dashed #a3e4d7; border-radius: 8px; padding: 20px; text-align: center; }
.cgpa-value { font-size: 42px; font-weight: bold; color: #27ae60; margin: 5px 0;}
.btn-save { background-color: #27ae60; color: white; margin-top: 10px; }
</style>