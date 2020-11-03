<template>
  <div id="app" :class="typeof weather.main!='undefined' && weather.main.temp > 16 ? 'warm':''">
    <main>
      <div class="search-box">
        <input type="name"
         placeholder="Search..." 
         class="search-bar" 
         v-model="query"
         @keypress="fetchData"
         
         />
        
      
      </div>
      <div class="weather-wrap" v-if="typeof weather.main!='undefined'">
      
        <div class="loc-box">
          
            <div class="location">{{weather.name}}, {{weather.sys.country}}

            </div>
            <div class="date">{{dateBuilder()}}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}° C <Cc:ie></Cc:ie></div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div><!--  -->
      </div> 
    </main>
  </div>

</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "fe8e359bb02783ab0729f1d06233bbfb",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchData(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
      console.log(results);
    },
    dateBuilder() {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;

    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
#app {
  background-image: url("https://user-images.githubusercontent.com/25447240/97994145-ff7fbd80-1e0a-11eb-998c-faabc49bf002.png");
  background-attachment: scroll;
  background-size: cover;
  background-position: bottom;
  transition: o.2s;
}
#app.warm {
  background-image: url("https://user-images.githubusercontent.com/25447240/97994130-fc84cd00-1e0a-11eb-987e-4a4aa1e19eb7.jpg");
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.45));
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  margin: none;
  outline: none;
  appearance: none;
  border: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  border-radius: 0px 16px 0px 16px;
  background-color: rgba(255, 255, 255, 0.5);
  transition: 0.4s;
}
.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  border-radius: 16px 0px 16px 0px;
}
.loc-box .location {
  text-align: center;
  font-size: 32px;
  font-weight: 500;
  color: white;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.loc-box .date {
  text-align: center;
  font-size: 20px;
  font-style: italic;
  font-weight: 250;
  color: white;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
