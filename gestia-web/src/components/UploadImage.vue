<template>
  <div>
    <el-upload
      v-model:file-list="fileList"
      :auto-upload="false"
      action="http://localhost:9090/v1/images/"
      list-type="picture-card"
      :on-success="handleSuccess"
      :on-preview="handlePictureCardPreview"
      :on-remove="handleRemove"
      ref="uploadRef"
    >
      <el-icon><Plus /></el-icon>
    </el-upload>

    <el-dialog v-model="dialogVisible">
      <img w-full :src="dialogImageUrl" alt="Preview Image" />
    </el-dialog>

    <div class="actions">
      <el-button type="primary" @click="handleUpload">Загрузить</el-button>
      <el-button @click="clearFiles">Очистить</el-button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { Plus } from '@element-plus/icons-vue'

import type { UploadProps, UploadUserFile } from 'element-plus'

const fileList = ref<UploadUserFile[]>([])
const dialogImageUrl = ref('')
const dialogVisible = ref(false)
const uploadRef = ref()

const handleRemove: UploadProps['onRemove'] = (uploadFile, uploadFiles) => {
  console.log('Удалён файл:', uploadFile)
  console.log('Оставшиеся файлы:', uploadFiles)
}

const handlePictureCardPreview: UploadProps['onPreview'] = (uploadFile) => {
  dialogImageUrl.value = uploadFile.url!
  dialogVisible.value = true
}

const handleUpload = () => {
  if (!fileList.value.length) {
    return console.warn('Нет файлов для загрузки')
  }
  uploadRef.value?.submit()
}

const handleSuccess = (response: any, file: UploadUserFile, fileListArray: UploadUserFile[]) => {
  console.log('Загрузка завершена:', file.name)
  fileList.value = fileListArray.filter(f => f.uid !== file.uid)
}

const clearFiles = () => {
  fileList.value = []
}
</script>

<style scoped>
.el-upload__picture-card-wrapper {
  position: relative;
}

.el-upload__picture-card-wrapper .success-icon {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0);
  color: var(--primary-color);
  font-size: 3rem;
  animation: success-bounce 0.8s forwards;
}

@keyframes success-bounce {
  0% {
    transform: translate(-50%, -50%) scale(0);
    opacity: 0;
  }
  50% {
    transform: translate(-50%, -50%) scale(1.2);
    opacity: 1;
  }
  100% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
  }
}
</style>
