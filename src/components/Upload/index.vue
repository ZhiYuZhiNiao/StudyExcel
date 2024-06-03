<template>
  <el-upload
    drag
    :before-upload="beforeUpload"
  >
    <el-icon class="el-icon--upload"><upload-filled /></el-icon>
    <div class="el-upload__text">
      请拖拽excel文件, 或者<em> 点击进行选取excel文件</em>
    </div>
    <template #tip>
      <div class="el-upload__tip">
        
      </div>
    </template>
  </el-upload>
</template>
<script setup>
import { ref, reactive } from 'vue'
import { UploadFilled } from '@element-plus/icons-vue'
import exceljs from 'exceljs'
import FileSaver from 'file-saver'

const fileReader = new FileReader()

/** @type {import('element-plus').UploadProps['beforeUpload']} */
const beforeUpload = (rawFile) => {
  console.log('rawFile = ', rawFile)
  fileReader.readAsArrayBuffer(rawFile)
}

fileReader.onloadstart = () => {
    console.log('开始读取')
}

fileReader.onload = async () => {
  console.log('读取成功')
  const { result } = fileReader
  const workbook = new exceljs.Workbook()
  await workbook.xlsx.load(result)
  console.log('workbook = ', workbook)
  const sheet1 = workbook.getWorksheet(1)
  console.log('workbook1 = ', sheet1)
  const cell = sheet1.getCell(1, 1)
  console.log('cell = ', cell)


  const _workbook = new exceljs.Workbook();
  const _worksheet = _workbook.addWorksheet('测试1')
  _worksheet.addRow([cell.value])
  // 导出表格文件
  _workbook.xlsx.writeBuffer().then((buffer) => {
    const file = new Blob([buffer], {type: 'application/octet-stream'});
    FileSaver.saveAs(file, 'ExcelJSzz.xlsx');
  }).catch(error => console.log('Error writing excel export', error))
}

fileReader.onloadend = () => {
  console.log('读取结束')
  console.log('fileReader = ', fileReader)
}

</script>
<style lang="scss" scoped>
</style>
