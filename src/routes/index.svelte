<script>
  import Map from "../components/Map.svelte";
	import AutoComplete from "../components/Autocomplete.svelte";
	import { marker } from '../components/stores.js';

  const asyncData = event => {
    console.log(event);
  };

	let event = null;

	// window.ee = new EventEmitter();

  function loadApiData(event) {
    console.log("loadApiData");
    if (event && event.target) {
      console.log("handleClick", event.target.value);
    }
	}
	
	function handleMessage(event) {
		console.log("handleMessage drawMarker", event.detail);
		marker.update(m => m = event.detail);
	}
</script>

<style>
  h1 {
    text-align: center;
    margin: 0 auto;
  }

  h1 {
    font-size: 2.8em;
    text-transform: uppercase;
    font-weight: 700;
    margin: 0 0 0.5em 0;
  }

  @media (min-width: 480px) {
    h1 {
      font-size: 4em;
    }
  }
</style>

<svelte:head>
  <title>Sapper project template</title>
</svelte:head>

<h1>Great success!</h1>

<AutoComplete name="countries" isAsync on:input={loadApiData(event)} on:drawMarker={handleMessage}>
  <div class="notification">Loading data from API...</div>
</AutoComplete>
<Map />
