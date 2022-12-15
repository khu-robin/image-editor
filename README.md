# Capstone Design 1 2022-2
# 빅데이터 기반 이미지 편집 온라인 솔루션
* 2019102173 박병창
* 2018102238 조인화

## Overview
SNS가 활성화되고 있는 요즘, 이미지에 대한 빅데이터가 기하급수적으로 증가하고 있다. 또한 빅데이터는 몇 년 전 클라우드 컴퓨팅 등과 함께 큰 주목을 받으며 등장한 이후, 최근 국내외에서 4차 산업혁명의 핵심기술로 급부상하고 있다. 따라서 본 문서는 빅데이터를 기반으로 하며 이미지 로드, 자르기, 뒤집기, 회전, 크기 조정, 그리기 등 다양한 기능을 지원하는 이미지 편집 온라인 솔루션을 제안하고 구현한다.

## Results
### 서버 실행
```bash
yarn serve
```
### 모듈로 사용
```vue
<template>
  <ImageEditor ref="imageEditor"/>
</template>
<script>
import { ImageEditor } from '(경로)/src/components/ImageEditor.vue'

export default {
  components: {
    ImageEditor
  },
  methods: {
    loadImage() {
      this.$refs.imageEditor.loadImage('https://example.com/image.png')
    }
  }
}
</script>
```
## Reports
* [Report](Report/최종보고서/%5BKHUmage%5D%20최종보고서.pdf)
