<template>
  <div>
    <el-upload
        class="avatar-uploader"
        action="http://localhost:6601/user/uploadAvatar"
        :with-credentials="true"
        method="put"
        :show-file-list="false"
        :on-success="handleAvatarSuccess"
        :before-upload="beforeAvatarUpload"
    >
      <img v-if="imageUrl" :src="imageUrl" class="avatar" alt=""/>
      <el-icon v-else class="avatar-uploader-icon"></el-icon>
    </el-upload>
  </div>
</template>

<script setup>
import {ref} from 'vue'
import {ElMessage} from 'element-plus'
import {uploadAvatar} from "@/apis/user.js";
import {Plus} from '@element-plus/icons-vue'

const imageUrl = ref('')

const handleAvatarSuccess = (response, uploadFile) => {
  imageUrl.value = URL.createObjectURL(uploadFile.raw)
  console.log("上传成功", imageUrl.value)
}

const beforeAvatarUpload = (rawFile) => {
  /* if (rawFile.type !== 'image/jpeg') {
     ElMessage.error('Avatar picture must be JPG format!')
     return false
   } else*/
  if (rawFile.size / 1024 / 1024 > 2) {
    ElMessage.error('Avatar picture size can not exceed 2MB!')
    return false
  }
  return true
}
</script>

<style scoped>
.avatar-uploader .avatar {
  width: 178px;
  height: 178px;
  display: block;
}
</style>

<style>
.avatar-uploader .el-upload {
  border: 1px dashed var(--el-border-color);
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  transition: var(--el-transition-duration-fast);
}

.avatar-uploader .el-upload:hover {
  border-color: var(--el-color-primary);
}

.el-icon.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  text-align: center;
}
</style>
