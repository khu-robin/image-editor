<template>
  <div ref="imageEditor" :style="{width: `${width}px`, height: `${height}px`}"></div>
  <template v-if="mode === 'normal'">
    <div class="btn-group" role="group">
      <button type="button" class="btn btn-outline-primary" @click="onCrop"><i class="bi bi-crop"></i></button>
      <button type="button" class="btn btn-outline-primary" @click="onRotate"><i class="bi bi-arrow-counterclockwise"></i></button>
      <button type="button" class="btn btn-outline-primary" @click="onEnterShape"><i class="bi bi-pentagon"></i></button>
    </div>
  </template>

  <template v-else-if="mode === 'crop'">
    <button type="button" class="btn btn-outline-warning" style="margin-right: 10px;" @click="onBack"><i class="bi bi-arrow-left"></i></button>
    <div class="btn-group" role="group">
      <input type="radio" id="radio-crop-1" name="cropAspect" class="btn-check" @click="setCropAspect()" checked>
      <label class="btn btn-outline-secondary" for="radio-crop-1">자유 형태</label>
      <input type="radio" id="radio-crop-2" name="cropAspect" class="btn-check" @click="setCropAspect(1)">
      <label class="btn btn-outline-secondary" for="radio-crop-2">1:1</label>
      <input type="radio" id="radio-crop-3" name="cropAspect" class="btn-check" @click="setCropAspect(4/3)">
      <label class="btn btn-outline-secondary" for="radio-crop-3">4:3</label>
      <input type="radio" id="radio-crop-4" name="cropAspect" class="btn-check" @click="setCropAspect(16/9)">
      <label class="btn btn-outline-secondary" for="radio-crop-4">16:9</label>
    </div>
    <button type="button" class="btn btn-outline-primary" style="margin-left: 10px;" @click="onApply"><i class="bi bi-check"></i></button>
  </template>
  <template v-else-if="mode === 'shape'">
    <button type="button" class="btn btn-outline-warning" style="margin-right: 10px;" @click="onBack"><i class="bi bi-arrow-left"></i></button>
    <div class="btn-group" role="group">
      <button type="button" class="btn" :class="ifClass(shape === 'rect', 'btn-secondary', 'btn-outline-secondary')" @click="setShape('rect')"><i class="bi bi-square"></i></button>
      <button type="button" class="btn" :class="ifClass(shape === 'circle', 'btn-secondary', 'btn-outline-secondary')" @click="setShape('circle')"><i class="bi bi-circle"></i></button>
      <button type="button" class="btn" :class="ifClass(shape === 'triangle', 'btn-secondary', 'btn-outline-secondary')" @click="setShape('triangle')"><i class="bi bi-triangle"></i></button>
    </div>
    <span>
      <input type="color" :value="foregroundColor" @change="onChangeColor($event, 'foregroundColor')">
      <input type="color" :value="backgroundColor" @change="onChangeColor($event, 'foregroundColor')">
    </span>
  </template>
</template>
<script>
import ImageEditor from 'tui-image-editor';

let imageEditor;

export default {
  name: 'ImageEditor',
  props: {
    width: {
      type: Number,
      default: 600
    },
    height: {
      type: Number,
      default: 500
    }
  },
  data() {
    return {
      mode: 'normal',
      imageWidth: 0,
      imageHeight: 0,
      cropAspect: 0,
      shape: '',
      foregroundColor: '#000000',
      backgroundColor: '#ffffff'
    };
  },
  methods: {
    ifClass(cond, ifTrue, ifFalse) {
      return {
        [ifTrue]: cond,
        [ifFalse]: !cond
      };
    },
    loadImage(f) {
      imageEditor.loadImageFromFile(f);
    },
    onCrop() {
      imageEditor.startDrawingMode('CROPPER');
      this.mode = 'crop';
      this.cropAspect = 0;
    },
    setCropAspect(ratio = 0) {
      imageEditor.setCropzoneRect(ratio);
      this.cropAspect = ratio;
    },
    onRotate() {
      imageEditor.rotate(-90);
    },
    onEnterShape() {
      imageEditor.startDrawingMode('SHAPE');
      this.mode = 'shape';
      this.shape = '';
    },
    updateShape() {
      imageEditor.setDrawingShape(this.shape, {
        stroke: this.foregroundColor,
        fill: this.backgroundColor
      });
    },
    setShape(shape) {
      this.shape = shape;
      this.updateShape();
    },
    onChangeColor(e, color) {
      this[color] = e.target.value;
      this.updateShape();
    },
    onBack() {
      imageEditor.stopDrawingMode();
      this.mode = 'normal';
    },
    onApply() {
      if(this.mode === 'crop') {
        imageEditor.crop(imageEditor.getCropzoneRect());
        imageEditor.stopDrawingMode();
        this.mode = 'normal';
      }
    }
  },
  mounted() {
    imageEditor = new ImageEditor(this.$refs.imageEditor, {
      cssMaxWidth: this.width,
      cssMaxHeight: this.height,
      usageStatistics: false,
    });
  }
};
</script>
<style lang="stylus">
@import '~tui-image-editor/dist/tui-image-editor.css'
</style>