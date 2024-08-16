<template>
  <div>
    <canvas ref="liveCanvas"></canvas>
    <div class="control">
      <button @click="handlerExpression('f00')">動作一</button>
      <button @click="handlerExpression('f01')">動作二</button>
      <button @click="handlerExpression('f02')">動作三</button>
      <button @click="handlerExpression('f03')">動作四</button>
      <button @click="handlerExpression('f04')">動作五</button>
      <button @click="handlerExpression('f05')">動作六</button>
      <button @click="handlerExpression('f06')">動作七</button>
      <button @click="handlerExpression('f07')">動作八</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import * as PIXI from 'pixi.js';
// @ts-ignore
import { Live2DModel } from 'pixi-live2d-display/cubism4';

(window as any).PIXI = PIXI;

let app: PIXI.Application;
let model: any;

const liveCanvas = ref(null);

onMounted(async () => {
  app = new PIXI.Application({
    view: liveCanvas.value || undefined,
    autoStart: true,
    // resizeTo: window,
    width: 350,
    height: 500,
    backgroundAlpha: 0,
    autoDensity: true,
    antialias: true,
    resolution: window.devicePixelRatio
  });

  // model = await Live2DModel.from('./library/vts/hiyori_pro_t11.model3.json');
  model = await Live2DModel.from(
    'https://cdn.jsdelivr.net/gh/guansss/pixi-live2d-display/test/assets/haru/haru_greeter_t03.model3.json'
  );
  app.stage.addChild(model);
  model.scale.set(0.1);
});

onBeforeUnmount(() => {
  model?.destroy();
  app?.destroy();
});

const handlerExpression = (type: string) => {
  console.log('🚀 ~ handlerExpression ~ type:', type);
  model.expression(type);
};
</script>

<style scoped></style>
