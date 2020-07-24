<template>
  <view class="container">
    <view class="cropper-wrap">
      <image-cropper
        id="image-cropper"
        ref="cropper"
        :zoom="1"
        :angle="0"
        :max-zoom="3"
        :min-zoom="0.5"
        :src="src"
        @load="load"
        @error="errHandle"
        @cropped="cropped"
        @afterDraw="afterDraw"
        @beforeDraw="beforeDraw"
      />
    </view>
    <image
      :src="img"
      mode="aspectFit"
      style="position: absolute; bottom: 0;width: 400rpx;
    left: 0;"
    />
    <view class="ctrls-wrap">
      <view class="ctrl" @tap="selectImg">上传图片</view>
    </view>
  </view>
</template>
<script>
import ImageCropper from '@/components/kd/uniapp-nice-cropper/src/cropper.vue'
// import ImageCropper from '@/components/kd/cropper/cropper.vue'

export default {
  components: {
    ImageCropper
  },
  data() {
    return {
      src: '',
      img: ''
    }
  },
  onLoad(opts) {

  },
  methods: {
    load(path, info) {
      console.log(path, info)
      setTimeout(() => {
        // 0.5秒钟后自动旋转45度
        // this.$refs.cropper.setRotate(45)
      }, 500)
    },
    beforeDraw(context, transform) {
      context.setFillStyle('yellow')
      // transform.zoom = 2
    },
    afterDraw(ctx, info) {
      ctx.setFillStyle('red')
      ctx.fillText('我是一行小水印', info.width - 100, info.height - 20)
    },
    cropped(e) {
      console.log(e)
      this.img = e
    },
    errHandle(e) {
      console.log('图片加载失败了')
    },
    selectImg() {
      uni.chooseImage({
        count: 1,
        sizeType: ['original'],
        sourceType: ['album', 'camera'],
        success: res => {
          var tempFilePaths = res.tempFilePaths
          this.src = tempFilePaths[0]
        }
      })
    }

  }
}
</script>
<style>
page {
  height: 100%;
  overflow: hidden;
  background: #000;
  /* #ifdef MP-ALIPAY */
  position: absolute;
  width: 100%;
  /* #endif */
}
</style>
<style lang="scss" scoped>
.container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  & .cropper-wrap {
    // flex: 1;
    height: 50%;
  }
  & .ctrls-wrap {
    display: flex;
    color: white;
    font-size: 34rpx;
    text-align: center;
    line-height: 96rpx;
    border-bottom: 1px solid #FFF;
    height: 96rpx;
    & .ctrl {
      flex: 1;
      flex-basis: 0;
    }
  }
}
</style>
