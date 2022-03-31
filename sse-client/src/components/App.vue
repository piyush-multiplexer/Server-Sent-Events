<template>
  <div id="app">
    <table class="stats-table">
      <thead>
        <tr>
          <th>Fact</th>
          <th>Source</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="fact in facts">
          <td>{{ fact.info }}</td>
          <td>{{ fact.source }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      facts: []
    };
  },
  mounted() {
    const events = new EventSource("http://localhost:3000/events");
    events.onmessage = event => {
      const parsedData = JSON.parse(event.data);
      this.facts.push(parsedData);
    };
  }
};
</script>

<style>
code {
  font-family: Courier New, monospace, serif;
  font-size: 0.9em;
  white-space: pre-wrap;
  color: #2c3e50;
}

body {
  color: #555;
  font-size: 25px;
  line-height: 1.5;
  margin: 0 auto;
  max-width: 50em;
  padding: 4em 1em;
}

.stats-table {
  border-collapse: collapse;
  text-align: center;
  width: 100%;
}

.stats-table tbody tr:hover {
  background-color: #f5f5f5;
}
</style>

<style scoped>
#app {
  text-align: center;
}
</style>
