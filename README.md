# test
<template>
  <div id="app">
    <div>
        <el-upload
          class="avatar-uploader"
          action="https://jsonplaceholder.typicode.com/posts/"
          :show-file-list="false"
          :on-success="handleAvatarSuccess"
          :before-upload="beforeAvatarUpload">
          <i  class="el-icon-plus avatar-uploader-icon" v-show='imageUrl' ref='newUploader'></i>
        </el-upload>
        <div class="upload-view" v-if="imageUrl">
            <div class="img">
                <img :src="imageUrl" alt="">
            </div>
            
            <div class="mask" >
                <el-button type="primary" icon="el-icon-edit" circle @click='edit'></el-button>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        className:'none',
        imageUrl: 'http://img5.duitang.com/uploads/item/201405/24/20140524105402_VK2Rz.jpeg'
      };
    },
    methods: {
      handleAvatarSuccess(res, file) {
        this.imageUrl = URL.createObjectURL(file.raw);
      },
      edit(){
        this.$refs.newUploader.click();
        // document.getElementById('upload').click();
      },
      handlemouseover(){
        this.className='show'
      },
      handlemouseout(){
        this.className='none'
      },
      beforeAvatarUpload(file) {
        const isJPG = file.type === 'image/jpeg';
        const isLt2M = file.size / 1024 / 1024 < 2;

        if (!isJPG) {
          this.$message.error('上传头像图片只能是 JPG 格式!');
        }
        if (!isLt2M) {
          this.$message.error('上传头像图片大小不能超过 2MB!');
        }
        return isJPG && isLt2M;
      }
    }
  }
</script>

<style>
#app {
  font-family: Helvetica, sans-serif;
  text-align: center;
}
.avatar-uploader{
    width: 178px;
    height: 178px;
    margin: none;
}
.avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
   
  }
  .img{
    width: 100%;
    height: 100%;
    background: red;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
  .upload-view{
    width: 180px;
    height: 180px;
    overflow: hidden;
    position: absolute;
    top: 0;
  }
  .upload-view .mask{
    display: none;
  }
  .upload-view:hover .mask{
    display: block;
  }
  .upload-view img{
    max-width: 100%;
  }
  
  .mask{
    position: absolute;
    top: 0px;
    left: 0px;
    background: rgba(0,0,0,.5);
    width: 178px;
    height: 178px;
  }
  
</style>
