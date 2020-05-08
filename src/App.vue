<template>
  <div id="app">
    <h1>Random programmer puns</h1>
    <div class="text">
      <h2 @click="generator">{{ fact.title }}</h2>
      <p>{{ fact.description }}</p>
    </div>
    <a href="https://github.com/SalesmanUnknown">
      <i class="fab fa-github"></i>
    </a>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      fact: {},
      mycolor: "#" + ((Math.random() * 0xffffff) << 0).toString(16)
    };
  },
  components: {},
  mounted() {
    document.body.style.background = this.mycolor;
  },
  beforeMount() {
    axios({
      method: "get",
      url: "https://projects-eldar.herokuapp.com/projects/random",
      timeout: 10000,
      headers: {
        "Content-Type": "application/json"
      }
    })
      .then(response => {
        this.fact = response.data;
        console.log(this.fact);
      })
      .catch(err => {
        console.log("err", err);
        this.fact = {
          title: "",
          description: "There was a problem handling your request."
        };

        console.log(this.fact);
      });
  },
  methods: {
    generator: function() {
      this.mycolor = "#" + ((Math.random() * 0xffffff) << 0).toString(16);
      document.body.style.background = this.mycolor;

      axios({
        method: "get",
        url: "https://projects-eldar.herokuapp.com/projects/random",
        timeout: 10000, // Wait for 5 seconds
        headers: {
          "Content-Type": "application/json"
        }
      })
        .then(response => {
          this.fact = response.data;
          console.log(this.fact);
        })
        .catch(err => {
          console.log("err", err);
          this.fact = {
            title: "",
            description: "There was a problem handling your request."
          };

          console.log(this.fact);
        });
    }
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  transition: 0.5s ease;
}

#app {
  font-family: "Press Start 2P", cursive;
  min-height: 100vh;
  border: 25px solid #141313;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  background-color: mycolor;

  h1 {
    cursor: default;
    text-align: center;
  }

  h2 {
    cursor: pointer;
    font-weight: 700;
    font-size: 30px;
    padding-bottom: 20px;
    text-align: center;
    transition: 0.5s ease;
    &:hover {
      color: white;
    }
  }

  p {
    text-align: center;
    font-size: 19px;
    cursor: default;
  }
  a {
    text-decoration: none;
    color: currentColor;
  }
  i {
    cursor: pointer;
    font-size: 40px;
    transition: 0.5s ease;
    &:hover {
      opacity: 0.8;
      color: white;
    }
  }
}
</style>
