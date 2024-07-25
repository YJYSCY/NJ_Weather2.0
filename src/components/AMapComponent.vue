<template>
  <div id="container" style="width: 100%; height: 400px"></div>
</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader';

export default {
  name: 'AMapComponent',
  props: ['jwd'],
  data() {
    return {
      map: null,
      mapLoaded: false,
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      AMapLoader.load({
        key: 'd3d542e631b0febbc5ddcd2449e419e4',
        version: '2.0',
        plugins: [],
      })
        .then((AMap) => {
          this.map = new AMap.Map('container', {
            viewMode: '3D',
            zoom: 13,
          });
          this.mapLoaded = true;
          if (this.jwd) {
            this.setCenterBasedOnJwd();
          }
        })
        .catch((error) => {
          console.error('地图加载失败:', error);
        });
    },
    setCenterBasedOnJwd() {
      if (this.map && this.mapLoaded && this.jwd) {
        try {
          switch (this.jwd) {
            case '':
              this.map.setCenter([118.796624, 32.059344]);
              break;
            case '320115':
              this.map.setCenter([118.83951, 31.953195]);
              break;
            case '320102':
              this.map.setCenter([118.797779, 32.048644]);
              break;
            case '320111':
              this.map.setCenter([118.627165, 32.059796]);
              break;
            case '320104':
              this.map.setCenter([118.794792, 32.039065]);
              break;
            case '320106':
              this.map.setCenter([118.769943, 32.066814]);
              break;
            case '320105':
              this.map.setCenter([118.731642, 32.003343]);
              break;
            case '320113':
              this.map.setCenter([118.909117, 32.096423]);
              break;
            case '320114':
              this.map.setCenter([118.779087, 31.991291]);
              break;
            case '320117':
              this.map.setCenter([119.028414, 31.651108]);
              break;
            case '320118':
              this.map.setCenter([118.892074, 31.328678]);
              break;
            case '320116':
              this.map.setCenter([118.822241, 32.323235]);
              break;
            default:
              console.log('未知的 jwd 值:', this.jwd);
          }
        } catch (error) {
          console.error('设置中心点失败:', error);
        }
      }
    },
  },
  watch: {
    jwd(newVal) {
      if (newVal && this.mapLoaded) {
        this.setCenterBasedOnJwd();
      }
    },
  },
};
</script>

<style scoped>
/* 如果有需要，可以在这里添加 CSS 样式 */
</style>
