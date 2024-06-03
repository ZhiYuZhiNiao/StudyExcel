<template>
  <div class="app-container">
    <div class="upload-container">
      <Upload />
    </div>
  </div>
</template>

<script setup>
import Upload from '@/components/Upload/index.vue'

// import fs from 'fs'
// console.log('fs.readFileSync = ', fs.readFileSync)
// console.log('exceljs', exceljs)
</script>

<style scoped>
.upload-container {
  width: 65%;
  margin: 150px auto;
}
</style>
