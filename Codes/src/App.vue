<template>
  <input type="file" id="file-image" @change="uploadImage" accept=".jpg, .jpeg, .png">
  <ImageEditor ref="imageEditor"/>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.min.css';
import 'bootstrap-icons/font/bootstrap-icons.scss';
import ImageEditor from '@/components/ImageEditor';

export default {
  name: 'App',
  components: {
    ImageEditor
  },
  data() {
    return {
      image: null
    };
  },
  methods: {
    uploadImage(e) {
      this.$refs.imageEditor.loadImage(e.target.files[0]);

    }
  }
}
</script>

<style lang="scss">

</style>
