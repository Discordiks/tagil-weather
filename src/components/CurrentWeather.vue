<template>
  <div class="c_block">
    <select class="search" v-model="sel_city" @change="getWeather">
      <option value="0">Тагил</option>
      <option value="1">Салда</option>
      <option value="2">Токио</option>
      <option value="3">Рим</option>
      <option value="4">Пекин</option>
    </select>
<div class="w_gl_block">
    <div class="w_block">
      <p>Сегодня</p>
      <p :style="{ color: color}">{{ temp }} C</p>
      <img :src="getIcon" alt="">
      <p>{{ weather }}</p>
    </div>
    <div class="w_block">
      <p>Завтра</p>
      <p :style="{ color: color}">{{ temp }} C</p>
      <img :src="getIcon" alt="">
      <p>{{ weather }}</p>
    </div>
    <div class="w_block">
      <p>Послезавтра</p>
      <p :style="{ color: color}" >{{ temp }} C</p>
      <img :src="getIcon" alt="">
      <p>{{ weather }}</p>
    </div>
  </div>
  <div class="time">
    <p>Текущее время</p>
    <p id="time_1">{{ time }}</p>
  </div>
  </div>
  
</template>

<script>
export default {
  name: "CurrentWeather",
  data() {
    return {
      cities: [
        {
          lat: 57.913,
          lon: 60.559,
          name: "Tagil",
        },
        {
          lat: 58.048,
          lon: 59.974,
          name: "Salda",
        },
        {
          lat: 35.689,
          lon: 139.691,
          name: "Tokio",
        },
        {
          lat: 41.902,
          lon: 12.496,
          name: "Roma",
        },
        {
          lat: 39.901,
          lon: 116.391,
          name: "Pekin",
        },
      ],
      sel_city: 0,
      temp: 35,
      weather: "Дождь",
      time: "12:00",
      image: "",
      color:"",
    };
  },
  methods: {
    getWeather() {
      let url = new URL("https://api.openweathermap.org/data/2.5/weather");
      url.searchParams.append("appid", "49b48305d6060fad869859740e1f7b7d");
      url.searchParams.append("units", "metric");
      url.searchParams.append("lang", "ru");
      url.searchParams.append("lat", this.cities[this.sel_city].lat);
      url.searchParams.append("lon", this.cities[this.sel_city].lon);

      fetch(url)
        .then((response) => response.json())
        .then((json) => {
          this.temp = json.main.temp;
          this.weather = json.weather[0].description;
          let date = new Date((json.dt+json.timezone)*1000);
          this.time = ("0" + date.getUTCHours()).slice(-2)+":"+("0" +date.getUTCMinutes()).slice(-2);
          this.image = json.weather[0].icon;
          this.color="red";
          if(json.main.temp<0)
          {
            this.color="blue";
          }
        });
    },
  },
  mounted() {
    this.getWeather();
    setInterval(() => this.getWeather(), 100000);
  },
  computed: {
    getIcon() {
      return (
        "https://openweathermap.org/img/wn/" + this.image+ "@2x.png"
      );
    },
  },
};
</script>

<style>
.search {
  display: flex;
  justify-content: start;
  width: 40%;
  margin-bottom: 20px;
  margin-top: 20px;
  font-size: 18px;
}
.w_gl_block{
  display: flex;
  flex-direction: row;
  gap: 40px;
}
.w_block {
  background-color: lightgray;
  padding: 20px;
  width: 170px;
}
.c_block {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.time{
  font-size: 20px;
}
#time_1{
  color: blueviolet;
  font-size: 26px;
}
</style>