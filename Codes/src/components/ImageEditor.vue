<template>
  <div ref="imageEditor" :style="{width: `${width}px`, height: `${height}px`}"></div>
  <UIMain/>
</template>
<script>
import ImageEditor from 'tui-image-editor';
import UIMain from './ui/Main';

let imageEditor;

export default {
  name: 'ImageEditor',
  components: {
    UIMain
  },
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
  methods: {
    loadImage(f) {
      console.log('loadImage', f);
      imageEditor.loadImageFromFile(f);
    },
    onCrop() {
      imageEditor.startDrawingMode('CROPPER');
    },
    onRotate() {
      imageEditor.rotate(-90);
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