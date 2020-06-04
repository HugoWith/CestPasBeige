<template>
  <div class="hello">
    <h1>balalala</h1>
    <div v-for="(record, index) in fullArray" :key="index">
      <!-- <p>{{fullArray[Math.floor(Math.random() * fullArray.length)].Citations}}</p> -->
      <p>
        {{ record.Citations }} -
        {{ record.Auteur }}
      </p>
      <p></p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      fullArray: [],
      randomArray: []
    };
  },
  created() {
    this.getData();
  },
  mounted() {
    this.getRandomQuotes();
    console.log(this.fullArray.length);
    console.log(this.randomArray);
  },

  methods: {
    getData: function() {
      const view = "imported table";
      const app_id = "appy9OSW6WdE6Dlm0";
      const app_key = "Bearer keyYyXwDnUOjERzzD";
      const url = "https://api.airtable.com/v0/" + app_id + "/" + view;
      axios
        .get(url, {
          headers: { Authorization: app_key }
        })
        .then(response => {
          console.log(response.data.records);
          this.fullArray.push(response.data.records);
        })
        .catch(error => console.log(error));
    },
    getRandomQuotes: function() {
      this.randomArray = this.fullArray[
        Math.floor(Math.random() * this.fullArray.length)
      ];
    }
  }
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
