# vue-i-cropper 图片裁剪

## <font color="#dd0000">vue-i-cropper</font>

&nbsp;🐡&nbsp;图片裁剪

&nbsp;🎈&nbsp;裁剪生成图片的格式 ，默认生成截图框宽度，默认生成截图框高度

&nbsp;💓&nbsp;关注官方微信公众号“创维VR”，获取最新的VR设备内容

## 技术选型
 ###  前端技术选型
  vue ^2.5+ [vue 轻型前端框架]  
  element ^2.10.1  [element 界面布局UI]  
  vue-cropper ^0.4.9 [vue 图片裁剪组建]
                              ......
  
## 预览

![Image text](https://skyworthxr-cms.oss-cn-shenzhen.aliyuncs.com/test/dHrrE9WBu0VjwYnbbgiz)  
![Image text](https://skyworthxr-cms.oss-cn-shenzhen.aliyuncs.com/test/S3ZXgONGxHBKoEVvZ5mq)  
![Image text](https://skyworthxr-cms.oss-cn-shenzhen.aliyuncs.com/test/gaRaKjNuOpcD7mus6J3X)  
## Build Setup

``` bash
# install dependencies
  npm i vue-i-cropper
  npm i vue-cropper 

  import Vueicropper from 'vue-i-cropper';

  <Vueicropper
    :option='option'
    :fixedNumber="fixedNumber"
  ></Vueicropper>

```

## 环境依赖
  "node": ">= 6.0.0"   
  "npm": ">= 3.0.0"  

## 配置（修改）
```
  fixedNumber: [9, 2], 
 option: {
    img: '', // 裁剪图片的地址  (默认：空)
    outputSize: 1, // 裁剪生成图片的质量  (默认:1)
    full: false, // 是否输出原图比例的截图 选true生成的图片会非常大  (默认:false)
    outputType: 'png', // 裁剪生成图片的格式  (默认:jpg) LOGO建议png
    canMove: true, // 上传图片是否可以移动  (默认:true)
    original: false, // 上传图片按照原始比例渲染  (默认:false)
    canMoveBox: true, // 截图框能否拖动  (默认:true)
    autoCrop: true, // 是否默认生成截图框  (默认:false)
    autoCropWidth: 480, // 默认生成截图框宽度  (默认:80%)
    autoCropHeight: 320, // 默认生成截图框高度  (默认:80%)
    fixedBox: false, // 固定截图框大小 不允许改变  (默认:false)
    fixed: true, // 是否开启截图框宽高固定比例  (默认:true)
    fixedNumber: [1, 1], // 截图框比例  (默认:[1:1])
    enlarge: 1
  }
  uploadFile ：function  =>{
    父组件接受裁剪的file 进行后续的逻辑操作
  }
```
