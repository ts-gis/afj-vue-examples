<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import ArcGISMap from "@arcgis/core/Map";
import SceneView from "@arcgis/core/views/SceneView";
import IntegratedMeshLayer from "@arcgis/core/layers/IntegratedMeshLayer"

import { onMounted } from 'vue'

onMounted(() => {
  const map = new ArcGISMap({
    basemap: "streets-vector"
  });

  const layer = new IntegratedMeshLayer({
    url: "http://localhost:8080/nlsc.slpk/SceneServer/layers/0",
    // Frankfurt integrated mesh data provided by nFrames and Aerowest
    copyright: "nFrames - Aerowest",
    title: "Integrated Mesh Frankfurt"
  });

  map.layers.add(layer);

  const view = new SceneView({
    map: map,
    container: "viewDiv",
    center: [ 13.157418390358545,32.8791384670639],
    zoom: 15,
  });

  view.when(() => {
    console.log("Map is loaded");
  })

  view.ui.remove('attribution')//清楚底部powered by ESRI
})


</script>

<template>
  <div id="viewDiv"></div>
</template>

<style>
#app {
  width: 100%;
  height: 100%;
}

html,
body {
  margin: 0;
  height: 100%;
  width: 100%;
}

#viewDiv {
  width: 100%;
  height: 100%;
}

/* 去除mapview拖动时的边框 */
.esri-view .esri-view-surface--inset-outline:focus::after {
  outline: auto 0px Highlight !important;
  outline: auto 0px -webkit-focus-ring-color !important;
}
</style>
