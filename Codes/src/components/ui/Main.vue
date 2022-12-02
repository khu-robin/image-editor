<template>
  <div class="btn-group" role="group" aria-label="Basic outlined example">
    <button type="button" class="btn btn-outline-primary" @click="$emit('crop')"><i class="bi bi-crop"></i></button>
    <button type="button" class="btn btn-outline-primary" @click="$emit('rotate')"><i class="bi bi-arrow-counterclockwise"></i></button>
  </div>
</template>
<script>
export default {
  name: 'UIMain'
};
</script>