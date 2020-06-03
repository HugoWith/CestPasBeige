<template>
  <div class="hello">
    <h1>balalala</h1>
    <p v-for="(record, index) in records" :key="index">{{ record.Citation }}</p>
    <p v-for="(record, index) in records" :key="index">{{ record.Auteur }}</p>
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
  mounted() {
    this.getData();
    console.log(this.fullArray);
  },
  methods: {
    getData: function() {
      var Airtable = require("airtable");
      var base = new Airtable({ apiKey: "keyYyXwDnUOjERzzD" }).base(
        "appy9OSW6WdE6Dlm0"
      );

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
              console.log(fullQuotes);

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
      //   let appId = "appy9OSW6WdE6Dlm0";
      //   let appName = "beige";
      //   let appKey = "keyspU26TtuKilc1K";
      //   // let url = "https://api.airtable.com/v0/" + appId + "/" + appName;
      //   // let axiosConfig = {
      //   //   headers: {
      //   //     Authorization: "Bearer " + appKey,
      //   //     "Content-Type": "application/json",
      //   //   },
      //   // };
      //   axios
      //     .get("https://api.airtable.com/v0/" + appId + "/" + appName, {
      //       headers: { Authorization: "Bearer " + appKey },
      //     })
      //     .then((resp) => {
      //       console.log(resp);
      //     })
      //     .catch((error) => console.log(error));
    },
  },
};
//   axios
//     .get(
//       `https://api.airtable.com/v0/${this.airTableApp}/${this.airTableName}`,
//       {
//         headers: { Authorization: "Bearer " + this.apiToken },
//       }
//     )
//     .then((res) => {
//       console.log(res);
//       this.records = res.data.records;
//       console.log(this.records);
//     });
// },
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
