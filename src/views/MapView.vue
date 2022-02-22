<script>
/* global mapboxgl */
export default {
  data: function () {
    return {
      places: [
        { lat: -25.363, lng: 131.044, description: "A place in Australia" },
        { lat: -33.8675, lng: 151.207, description: "The main city!" },
      ],
    };
  },
  mounted: function () {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_ACCESS_TOKEN;
    const map = new mapboxgl.Map({
      container: "map", // container ID
      style: "mapbox://styles/mapbox/navigation-night-v1", // style URL
      center: [-110.623177, 45.881832], // starting position [lng, lat]
      zoom: 6, // starting zoom
    });
    console.log(map);
    const popup = new mapboxgl.Popup({ offset: 25 }).setText(
      "This is a Nice as well"
    );
    console.log(popup);
    const marker1 = new mapboxgl.Marker()
      .setLngLat([-126.210289, 47.121235])
      .setPopup(popup)
      .addTo(map);
    console.log(marker1);
    const popup2 = new mapboxgl.Popup({ offset: 25 }).setText("This is Nice");
    console.log(popup2);

    const marker2 = new mapboxgl.Marker({ color: "black", rotation: 45 })
      .setLngLat([12.65147, 55.608166])
      .setPopup(popup2)
      .addTo(map);
    console.log(marker2);

    //hard coded location from places

    const marker3 = new mapboxgl.Marker({ color: "black", rotation: 45 })
      .setLngLat([this.places[0].lng, this.places[0].lat])
      .addTo(map);
    console.log(marker3);

    this.places.forEach((place) => {
      console.log("Heres a place", place);
      new mapboxgl.Marker({ color: "black", rotation: 45 })
        .setLngLat([place.lng, place.lat])
        .setPopup(new mapboxgl.Popup({ offset: 25 }).setText(place.description))
        .addTo(map);
    });
  },
};
</script>

<template>
  <div class="map">
    <h2>MapBox Test</h2>
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  width: 100%;
  height: 500px;
}
</style>
