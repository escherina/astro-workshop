<template>
  <section>
    <h2>ISS current location</h2>

    <p v-if="location">
      {{ location.latitude }}, {{ location.longitude }}
    </p>
    <p v-else>Location unknown.</p>

    <button @click="fetchIssLocation">Update location</button>
  </section>
</template>

<script>
export default {
  name: 'IssLocation',

  data() {
    return {
      location: null
    }
  },

  mounted() {
    this.fetchIssLocation()
  },

  methods: {
    async fetchIssLocation() {
      const response = await fetch('http://api.open-notify.org/iss-now.json')
      const { iss_position } = await response.json()
      this.location = iss_position
    }
  }
}
</script>

<style scoped>
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
