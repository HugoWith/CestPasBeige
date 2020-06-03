<template>
  <div class="hello">
    <h1>balalala</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      apiUrl: "https://api.airtable.com/v0/",
      apiToken: "keyUzWURiz5JP5KbA", // Always use a read-only account token
      airTableApp: "appy9OSW6WdE6Dlm0",
      airTableName: "beige",
      records: [],
    };
  },
  mounted() {
    console.log(process.env.VUE_APP_AIRTABLEKEY);
    console.log("coucou");

    this.getData();
  },
  methods: {
    getData: function() {
      axios
        .get(
          `https://api.airtable.com/v0/${this.airTableApp}/${this.airTableName}`,
          {
            headers: { Authorization: "Bearer " + this.apiToken },
          }
        )
        .then((res) => {
          console.log(res);
          this.records = res.data.records;
          console.log(this.records);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
