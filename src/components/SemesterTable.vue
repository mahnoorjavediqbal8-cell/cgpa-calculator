<template>
  <div class="semester-row">
    <span class="sem-label">Semester {{ index + 1 }}</span>
    <div class="inputs-flex">
      <input 
        type="number" 
        :value="semester.gpa" 
        @input="$emit('update-data', index, 'gpa', $event.target.value)"
        placeholder="GPA (e.g. 3.80)" 
        min="0" max="4" step="0.01" 
      />
      <input 
        type="number" 
        :value="semester.credits" 
        @input="$emit('update-data', index, 'credits', $event.target.value)"
        placeholder="Credits (e.g. 15)" 
        min="1" 
      />
      <button @click="$emit('remove-semester', index)" class="btn-delete" type="button">🗑️</button>
    </div>
  </div>
</template>

<script setup>
// Props incoming layer
defineProps({
  semester: Object,
  index: Number
})

// Custom Emit definitions
defineEmits(['update-data', 'remove-semester'])
</script>

<style scoped>
.semester-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px 0;
  border-bottom: 1px solid #eaeded;
}
.sem-label {
  font-weight: 600;
  color: #34495e;
}
.inputs-flex {
  display: flex;
  gap: 15px;
}
input {
  padding: 10px;
  border: 1px solid #ced4da;
  border-radius: 6px;
  width: 130px;
  transition: border-color 0.2s;
}
input:focus {
  border-color: #d35400;
  outline: none;
}
.btn-delete {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 18px;
  transition: transform 0.2s;
}
.btn-delete:hover {
  transform: scale(1.15);
}
</style>