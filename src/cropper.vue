<template>
  <view class="nice-cropper" :style="{height: height, width: width, background: background}" @touchstart="start" @touchmove.stop="move" @touchcancel="end" @touchend="end">
    <image class="nice-cropper__image" :src="src" :style="{transform: transformMeta, width: image.width + 'px', height: image.height + 'px'}" />
    <view class="nice-cropper__ctrls" :class="{'nice-cropper__ctrls--view' : view, 'nice-cropper__ctrls--border': showCtrlBorder, 'nice-cropper__ctrls--circle': view && circleView && maskType !== 'outline'}" :style="ctrlStyle">
      <view class="nice-cropper__corner nice-cropper__corner--lt" @touchstart="setCutMode('lt')" />
      <view class="nice-cropper__corner nice-cropper__corner--rt" @touchstart="setCutMode('rt')" />
      <view class="nice-cropper__corner nice-cropper__corner--rb" @touchstart="setCutMode('rb')" />
      <view class="nice-cropper__corner nice-cropper__corner--lb" @touchstart="setCutMode('lb')" />
    </view>
    <canvas v-if="canvasId" :id="canvasId" :canvas-id="canvasId" style="position: absolute;left:-500000px;top: -500000px" :style="{width: ctrlWidth * canvasZoom+'px', height: ctrlHeight * canvasZoom + 'px'}" />
  </view>
</template>
<script src="./cropper.js"></script>
<style>
.nice-cropper {
  position: relative;
  width: 100%;
  height: 100%;
  background: #000;
  overflow: hidden;
}
.nice-cropper__image {
  position: absolute;
  left: 0;
  top: 0;
  transform-origin: 50% 50%;
}
.nice-cropper__corner {
  width: 30rpx;
  height: 30rpx;
  position: absolute;
}
.nice-cropper__corner::after {
  position: absolute;
  left: -5px;
  right: -5px;
  bottom: -5px;
  top: -5px;
  content: '';
}
.nice-cropper__ctrls {
  position: absolute;
  box-shadow: inset 0 0 10rpx 0 rgba(0,0,0,.3);
}
.nice-cropper__ctrls--circle {
  border-radius: 50%;
}
.nice-cropper__ctrls--border {
  border: 2rpx solid #fff;
}
.nice-cropper__corner--lt {
  left: 0;
  top: 0;
  border-top: 4rpx solid #FFF;
  border-left: 4rpx solid #FFF;
}
.nice-cropper__corner--rt {
  right: 0;
  top: 0;
  border-top: 4rpx solid #FFF;
  border-right: 4rpx solid #FFF;
}
.nice-cropper__corner--rb {
  right: 0;
  bottom: 0;
  border-right: 4rpx solid #FFF;
  border-bottom: 4rpx solid #FFF;
}
.nice-cropper__corner--lb {
  left: 0;
  bottom: 0;
  border-left: 4rpx solid #FFF;
  border-bottom: 4rpx solid #FFF;
}
</style>
