<template>
  <div class="hello container">
    <h1 :class="{ bg : titleclicked }">"C'est pas beige,</h1>
    <h2 :class="{ bg : titleclicked }">C'est Blanc nature"</h2>
    <div class="container--main">
      <!-- <p>{{fullArray[Math.floor(Math.random() * fullArray.length)].Citations}}</p> -->
      <p class="citation" :class="{ bg : titleclicked }">{{ randomArray.Citations }}</p>
      <p class="auteur">{{ randomArray.Auteur }}</p>
    </div>
    <div class="container--btn">
      <button class="btn" v-on:click="getRandomQuotes">Une autre ? 🍾</button>
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
      randomArray: [],
      titleclicked: true
    };
  },
  created() {},
  mounted() {
    this.getData();
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
          // console.log(response.data.records);
          let rep = [];
          let minimiseAnswer = [];
          rep.push(response.data.records);
          this.offset = response.data.offset;
          rep.forEach(record => {
            record.forEach(e => {
              // console.log(e.fields);
              minimiseAnswer.push(e.fields);
            });
            // console.log(minimiseAnswer);
            this.fullArray = minimiseAnswer;
            this.getRandomQuotes();
          });
        })
        .catch(error => console.log(error));
    },
    getRandomQuotes: function() {
      let randomQuotes = this.fullArray[
        Math.floor(Math.random() * this.fullArray.length)
      ];
      this.randomArray = randomQuotes;
      this.titleclicked = !this.titleclicked;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.bg {
  background: rgb(0, 0, 0) !important;
  background: linear-gradient(
    131deg,
    rgba(0, 0, 0, 1) 0%,
    rgba(37, 40, 61, 1) 53%
  ) !important;
  background-clip: text !important;
  -webkit-background-clip: text !important;
  color: transparent !important;
}

h1,
h2 {
  font-family: "Montserrat", sans-serif;
  font-weight: Bold;
  text-align: start;
  text-transform: uppercase;
  color: #ffeddf;
}

h1 {
  font-size: 80px;
  overflow: hidden;
}

.blue {
  color: #bdd4e7;
}

h2 {
  font-size: 60px;
  transform: translateX(10%);
  margin-top: -15px;
}

.citation {
  font-family: "Lora", sans-serif;
  color: #25283d;
  font-size: 35px;
  text-align: center;
}
.auteur {
  font-family: "Lora", sans-serif;
  text-align: end;
  margin-top: 5%;
  color: #25283d;
  font-style: italic;
  font-weight: 400;
}

.container {
  max-width: 1750px;
  margin: 0 auto;
  height: 100vh;
  padding: 20px;
  overflow: hidden;
}

.container--main {
  // transform: translate(20%, 20%);
  width: 80%;
  margin: 10% auto 5% auto;
  overflow: hidden;
}

.container--btn {
  position: absolute;
  width: 90%;
  text-align: center;
  margin: 0 auto;
  bottom: 20%;
  overflow: hidden;
}
// transform: translateY(-100px);

.btn {
  width: 200px;
  border-radius: 30px;
  padding: 10px;
  cursor: pointer;
  margin: 0 auto;
  background-color: transparent;
  border: 1px solid #feea00;
  color: #ffeddf;
  font-size: 16px;
  font-weight: light;
  font-family: "Lora", sans-serif;
}
button:focus {
  outline: 0;
}

.btn:hover {
  animation: fill 0.5s forwards ease-in-out;
}

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

@keyframes fill {
  100% {
    background-color: #feea00;
    color: #25283d;
  }
}

@media (min-width: 1440px) {
}
@media (max-width: 1200px) {
  h1 {
    font-size: 5em;
  }
  h2 {
    font-size: 4em;
  }
}
@media (max-width: 992px) {
  h1 {
    font-size: 3em;
  }
  h2 {
    font-size: 2em;
  }
}
@media (max-width: 768px) {
  h1 {
    font-size: 2.5em;
    margin-bottom: 30px;
    text-align: start;
  }
  h2 {
    font-size: 1.8em;
  }
  .citation {
    font-size: 1.2em;
  }
  .auteur {
    font-size: 0.5em;
  }
  .btn {
    font-size: 0.5em;
  }
  .container--main {
    margin: 20% auto;
  }
  .container--btn {
    bottom: 5%;
  }
}
</style>
