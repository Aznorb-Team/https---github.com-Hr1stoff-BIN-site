<template>
  <div class="container">
    <Header />
    <Info />
    <Map />
    <!-- <Metrics /> -->
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';

import Info from '@/components/Info.vue';

import Map from '@/components/Map.vue';

import Footer from '@/components/Footer.vue';

import Metrics from '@/components/Metrics.vue';


export default {
  components: {
    Header,
    Info,
    Map,
    Footer,
    Metrics
  },
  data() {
    return {
      shops: [],
      currentPlacemarkCoords: null,
    };
  },
  mounted() {
    //this.initMap();
    this.loadShops();
  },
  methods: {
    loadShops() {
      fetch('shops.json')
        .then(response => response.json())
        .then(data => {
          this.shops = data;
        })
        .catch(error => {
          console.error('Ошибка при загрузке магазинов:', error);
        });
    },
    handlePlacemarkMoved(coords) {
      const radius = 500; 
      const filteredShops = this.shops.filter(shop => {
        return this.getDistanceBetweenPoints(
          coords,
          [shop.latitude, shop.longitude]
        ) <= radius;
      });

      console.log('Отфильтрованные магазины:', filteredShops);
    },

    getDistanceBetweenPoints(point1, point2) {
      const R = 6378137; 
      const dLat = this.degreesToRadians(point2[0] - point1[0]);
      const dLon = this.degreesToRadians(point2[1] - point1[1]);
      const a =
        Math.sin(dLat / 2) * Math.sin(dLat / 2) +
        Math.cos(this.degreesToRadians(point1[0])) * Math.cos(this.degreesToRadians(point2[0])) *
        Math.sin(dLon / 2) * Math.sin(dLon / 2);
      const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
      return R * c; 
    },

    degreesToRadians(degrees) {
      return degrees * (Math.PI / 180);
    }
  }
}
</script>

<style scoped></style>