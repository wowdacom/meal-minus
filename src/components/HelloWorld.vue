<template>
  <div class="hello max-w-screen-sm m-auto">
    <h1 class="text-center font-bold">Meal Minus</h1>
    <div class="map-dashboard flex">
      <div class="map w-3/5">
        <div id="main-map" class="block relative z-10 w-full h-full"></div>
      </div>
      <div class="point-of-foodimages w-2/5 flex flex-wrap">
        <div
          :key="item"
          v-for="item in 4"
          class="foodimages flex-shrink-0 w-1/2"
        >
          {{ item }}
        </div>
      </div>
    </div>
  </div>
</template>

<style>
@import "~leaflet/dist/leaflet.css";
@import "~leaflet.markercluster/dist/MarkerCluster.css";
@import "~leaflet.markercluster/dist/MarkerCluster.Default.css";
</style>

<script>
import L from "leaflet";
import { onMounted } from "vue";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  setup() {
    const mapInit = () => {
      const Layer_ID = "EMAP";
      const MAP_TYPE = {
        osm: `https://{s}.tile.osm.org/{z}/{x}/{y}.png`,
        nlsc: `https://maps.nlsc.gov.tw/S_Maps/wmts?SERVICE=WMTS&REQUEST=GetTile&VERSION=1.0.0&LAYER=${Layer_ID}&STYLE=_null&TILEMATRIXSET=EPSG:3857&TILEMATRIX=EPSG:3857:{z}&TILEROW={y}&TILECOL={x}&FORMAT=image/png`,
      };
      const map = L.map("main-map").setView([25.030284, 121.549201], 13);

      L.control.zoom({ position: "bottomright" }).addTo(map);

      L.tileLayer(MAP_TYPE["nlsc"], {
        maxZoom: 19,
        //attribution: `&copy; <a target="_blank" rel="noopener noreferrer" href="https://maps.nlsc.gov.tw/">內政部國土測繪中心</a>`
      }).addTo(map);
    };

    onMounted(() => {
      mapInit();
    });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  border: solid 1px red;
}
.foodimages {
  padding-bottom: 50%;
  height: 0;
}
</style>
