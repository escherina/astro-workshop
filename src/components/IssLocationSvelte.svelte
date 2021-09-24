<script>
  let location;

  async function fetchIssLocation() {
    const response = await fetch("http://api.open-notify.org/iss-now.json");
    const { iss_position } = await response.json();
    location = iss_position;
  }

  fetchIssLocation();
</script>

<section>
  <h2>ISS current location</h2>

  <p>
    {#if location}
      {location.latitude}, {location.longitude}
    {:else}
      Location unknown.
    {/if}
  </p>

  <button on:click={fetchIssLocation}>Update location</button>
</section>

<style>
  section {
    background-color: #171f31;
    margin-top: 2rem;
    padding: 1rem;
  }

  p {
    margin-block: 2rem;
  }

  button {
    background-color: #253048;
    border: 0;
    color: white;
    cursor: pointer;
    font-family: inherit;
    font-size: inherit;
    font-weight: bold;
    padding: 0.5rem;
    width: 100%;
  }

  button:hover,
  button:focus {
    background-color: #404e6b;
  }
</style>
