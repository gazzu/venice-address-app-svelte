<script>
  import { onMount } from "svelte";
  import { marker } from "../components/stores.js";

  let mymap = null;

  onMount(() => {
    const accessToken =
      "pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw";

    mymap = L.map("map").setView([45.505, 12.28], 13);

    L.tileLayer(
      "https://server.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer/tile/{z}/{y}/{x}",
      {
        attribution:
          "Tiles &copy; Esri &mdash; Source: Esri, DeLorme, NAVTEQ, USGS, Intermap, iPC, NRCAN, Esri Japan, METI, Esri China (Hong Kong), Esri (Thailand), TomTom, 2012"
      }
    ).addTo(mymap);
  });

  function listener(data) {
    if (data.loc) {
      const position = [data.loc.lat, data.loc.lng];
      mymap.setView(position, 16);
      L.marker(position)
        .bindPopup("<b>" + data.key + "</b>")
        .openPopup()
        .addTo(mymap);
    }
  }

  // window.ee.addListener("drawMarker", listener);

  const unsubscribe = marker.subscribe(value => {
    listener(value);
  });
</script>

<style>
  #map {
    height: 300px;
  }
</style>

<div id="map" />
