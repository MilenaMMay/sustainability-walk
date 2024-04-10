<script setup lang="ts">
import { onMounted } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

import 'leaflet/dist/leaflet.css'
import * as L from 'leaflet'
import type { LatLng } from 'leaflet'

const universityCologne: LatLng = L.latLng(50.928489708499356, 6.929532458566885)
const zoomLevel = 18 // maximum zoom level so that we start as close as possible
const minZoom = 15 // avoids that users zoom out of the relevant space

interface Place {
  name: string
  coordinates: LatLng
}

const places: Place[] = [
  { name: 'Phil Café', coordinates: L.latLng(50.92814086076388, 6.92777104434133) },
  { name: 'Bistro Uni E-Raum', coordinates: L.latLng(50.928439764085766, 6.929710116076665) }
]

onMounted(() => {
  var sustainabilityMap = L.map('map').setView(universityCologne, zoomLevel)
  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
    minZoom: minZoom
  }).addTo(sustainabilityMap)

  places.forEach((place) => {
    const marker = L.marker(place.coordinates).addTo(sustainabilityMap)
    marker.bindPopup(place.name)
  })
})
</script>

<template>
  <header>
    <!-- TODO: Logo University Cologne -->
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="Sustainability Walk Universitat zu Köln" />
    </div>
  </header>

  <div>
    <h2>TODO: Erklärung, was ist der Sustainability Walk?</h2>
    <div id="map" style="height: 60vh"></div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
