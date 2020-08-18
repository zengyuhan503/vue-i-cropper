<template>
  <div>
    <el-row :gutter="40">
      <el-col :span="12">
        <p style="text-align: right;">操作平台LOGO：</p>
      </el-col>
      <el-col :span="12">
        <el-upload class="avatar-uploader"
                   action=""
                   :on-change="handlelogChange"
                   :http-request="upLogoUrl"
                   :auto-upload='false'
                   :show-file-list="false"
                   :before-upload="beforelogoUpload">
          <div style="width: 320px;height: 71px;position:relative">
            <img v-if="ruleForm.logo"
                 :src="ruleForm.logo"
                 style="width:320px;height:71px;"
                 class="avatar">
            <i style="width:320px;height:71px; position: absolute;z-index: 9;top: 0;left: 0;line-height:71px"
               class="el-icon-plus avatar-uploader-icon"></i>
          </div>
        </el-upload>
      </el-col>
    </el-row>
    <el-dialog :visible.sync="cropperModel"
               width="1100px"
               :option='option'
               :before-close="beforeClose">
      <Cropper :imgFile="file"
               ref="vueCropper"
               :fixedNumber="fixedNumber"
               @upload="upload">
      </Cropper>
    </el-dialog>
  </div>
</template>
<script>

import Cropper from './cropper/cropper';
export default {
  components: {
    Cropper
  },
  props: {
    uploadFile: {
      type: Function,
      default: null
    }
    , fixedNumber: {
      type: Array,
      default: function () {
        return [9, 2]
      }
    },
    option: {
      type: Object,
      default: function () {
        return {
          img: '', // 裁剪图片的地址  (默认：空)
          outputSize: 1, // 裁剪生成图片的质量  (默认:1)
          full: false, // 是否输出原图比例的截图 选true生成的图片会非常大  (默认:false)
          outputType: 'png', // 裁剪生成图片的格式  (默认:jpg)
          canMove: true, // 上传图片是否可以移动  (默认:true)
          original: false, // 上传图片按照原始比例渲染  (默认:false)
          canMoveBox: true, // 截图框能否拖动  (默认:true)
          autoCrop: true, // 是否默认生成截图框  (默认:false)
          autoCropWidth: 480, // 默认生成截图框宽度  (默认:80%)
          autoCropHeight: 320, // 默认生成截图框高度  (默认:80%)
          fixedBox: false, // 固定截图框大小 不允许改变  (默认:false)
          fixed: true, // 是否开启截图框宽高固定比例  (默认:true)
          fixedNumber: [1.5, 1], // 截图框比例  (默认:[1:1])
          enlarge: 1
        }
      }
    }
  },
  data () {
    return {
      ruleForm: {
        logo: ""
      },
      file: "",
      cropperModel: false,
    }
  },
  methods: {
    dataURLtoFile (dataurl, filename) {
      var arr = dataurl.split(","),
        mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]),
        n = bstr.length,
        u8arr = new Uint8Array(n);
      while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
      }
      return new File([u8arr], filename, { type: mime });
    },
    beforeClose () {
      this.cropperModel = false;
    },
    upload (options) {
      var file = this.dataURLtoFile(options.data, options.file.name);
      this.ruleForm.logo = options.data;
      this.beforeClose()
      this.uploadFile(options)
    },
    handlelogChange (file, fileList) {
      this.uptype = 2;
      this.file = file
      this.cropperModel = true;
    },
    beforelogoUpload (file) {
      const isJPG = file.type === 'image/jpeg';
      const isLt2M = file.size / 1024 / 1024 < 20;
      if (!isJPG) {
        this.$message.error('上传封面图片只能是 JPG 格式!');
      }
      if (!isLt2M) {
        this.$message.error('上传封面图片大小不能超过 2MB!');
      }
      return isJPG && isLt2M;
    },
    upLogoUrl (file) {

    },
    resetLogo () {
      this.$confirm('你确定要清除该LOGO?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.vrliveinfo.logo = ""
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消操作'
        });
      });
    },
  },
  mounted () {

  },
}
</script>
<style lang="">
@import "./i-cropper.css";
</style>