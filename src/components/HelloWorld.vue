<template>
  <div class="hello">
    <h1>balalala</h1>
    <div v-for="(record, index) in fullArray" :key="index">
      <p>
        {{ record.Citations }} -
        {{ record.Auteur }}
      </p>
      <p></p>
    </div>
  </div>
</template>

<script>
// import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      fullArray: [],
    };
  },
  beforeMount() {
    this.getData();
  },
  mounted() {
    this.getRandomQuotes();
  },
  methods: {
    getData: function() {
      let Airtable = require("airtable");
      let base = new Airtable({ apiKey: "keyYyXwDnUOjERzzD" }).base(
        "appy9OSW6WdE6Dlm0"
      );
      let a = [];
      base("Imported table")
        .select({
          view: "Grid view",
        })
        .eachPage(
          function page(records) {
            // This function (`page`) will get called for each page of records.

            records.forEach(function(record) {
              // console.log(record.fields);

              let fullQuotes = record.fields;
              // console.log(fullQuotes);
              a.push(fullQuotes);

              // console.log("Retrieved", record.get("Citations"));
              // console.log("Retrieved", record.get("Auteur"));
            });

            // To fetch the next page of records, call `fetchNextPage`.
            // If there are more records, `page` will get called again.
            // If there are no more records, `done` will get called.
            // fetchNextPage();
          },
          function done(err) {
            if (err) {
              console.error(err);
              return;
            }
          }
        );

      this.fullArray = a;
    },
    getRandomQuotes: function() {
      console.log(this.fullArray.length);
      let randomQuote = this.fullArray[
        Math.floor(Math.random() * this.fullArray.length)
      ];
      console.log(randomQuote);
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
