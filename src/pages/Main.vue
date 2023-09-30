<template>
  <main class="main nuxt-pages">
    <div class="container">
      <h1 class="main title">Погода</h1>
      <div class="weather">
        <div class="weather__body">
          <div class="now" data-aos="fade-up">
            <h3>Сейчас</h3>
            <small class="white">{{ new Date().toLocaleTimeString() }}</small>
            <div class="now__weather">
              <div class="img__container">
                <img
                  :src="'http://openweathermap.org/img/w/' + iconcode + '.png'"
                  alt=""
                />
              </div>
              <div class="info__container">
                <div class="temp">
                  {{ degNow
                  }}<small
                    class="f-c-btn"
                    @click="
                      () => {
                        units = !units;
                        getData();
                        getDayWeather();
                        getFourDaysWeather();
                      }
                    "
                    >{{ units ? "F" : "C" }}</small
                  >
                </div>
                <hr />
                <div class="info__state">
                  <div class="state-now">Сейчас</div>
                  <div class="wind">
                    <img
                      src="https://shymbulak.com/_nuxt/img/wind.8842246.svg"
                      alt=""
                    />
                    {{ wind }} м/с
                  </div>
                  <div class="precipitation">
                    <img
                      src="https://shymbulak.com/_nuxt/img/precipitation.ada3750.svg"
                      alt=""
                    />
                    {{ humidity }} см
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-aos="fade-up">
            <div class="title">
              <h3>Погода в течение дня</h3>
            </div>
            <hr />
            <div class="day__container">
              <div class="arrow" @click="log">
                <img
                  src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iOSIgaGVpZ2h0PSIxNiIgdmlld0JveD0iMCAwIDkgMTYiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxwYXRoIGQ9Ik0wLjI1ODk0OSA4LjAwNDQzQzAuMjU4OTQ5IDguMTcwMTIgMC4zMjIyNzcgOC4zMzU5NyAwLjQ0ODc3MyA4LjQ2MjQ3TDYuOTI3NCAxNC45NDExQzcuMTgwNTYgMTUuMTk0MyA3Ljc2NjM4IDE1LjA5MzQgOC4wMTkzNyAxNC44NDAzQzguMjcyMzYgMTQuNTg3MSA4LjQxODc4IDEzLjk3MTggOC4xNjU2MyAxMy43MTg4TDIuMzIxMTQgOC4wMDQ0M0w4LjE2NTYzIDIuMjI1M0M4LjQxODc4IDEuOTcyMTQgOC4zMDcwNSAxLjM5NjYyIDguMDUzOSAxLjE0MzYzQzcuODAwNzQgMC44OTA2MzUgNy4xODAzOSAwLjgxNDYwNCA2LjkyNzQgMS4wNjc3NkwwLjQ0ODc3MyA3LjU0NjM5QzAuMzIyMjc3IDcuNjcyODggMC4yNTg5NDkgNy44Mzg3NCAwLjI1ODk0OSA4LjAwNDQzWiIgZmlsbD0iIzRGNTg2NCIvPgo8L3N2Zz4K"
                  alt=""
                />
              </div>
              <div id="day__container__wrapper" class="day__container__wrapper">
                <div class="item" v-for="item in dayWeather">
                  <div class="time">
                    {{ item.dt_txt.split(" ")[1].split(":")[0] }}
                  </div>
                  <div class="icon">
                    <img
                      :src="
                        'http://openweathermap.org/img/w/' +
                        item.weather[0].icon +
                        '.png'
                      "
                      alt=""
                    />
                  </div>
                  <div class="temperature">
                    <small class="temp-small">
                      {{ Math.floor(item.main.temp) }}
                      {{ units ? "°C" : "°F" }}</small
                    >
                  </div>
                </div>
              </div>
              <div class="arrow two" @click="log">
                <img
                  class="two"
                  src="https://shymbulak.com/_nuxt/img/arrow-right.7e85a2c.svg"
                  alt=""
                />
              </div>
            </div>
          </div>
        </div>
        <div class="weather_days" data-aos="fade-up" data-aos-duration="800">
          <div class="days">
            <div class="title">
              <h3>Погода на {{ fourDaysWeather.length }} дня(ей)</h3>
            </div>
            <div class="forecast">
              <div class="forecast_item" v-for="item in fourDaysWeather">
                <div class="date">
                  <!-- <div class="date-week"></div> -->
                  <div class="date-calendar">
                    {{ item.dt_txt.split(" ")[0] }}
                  </div>
                </div>
                <div class="weather-icon">
                  <img
                    :src="
                      'http://openweathermap.org/img/w/' +
                      item.weather[0].icon +
                      '.png'
                    "
                    alt=""
                  />
                  <div class="precipitation_probability">
                    {{ item.main.humidity }}%
                  </div>
                </div>
                <div class="segment">
                  <div class="segment-item">
                    мин.
                    <span
                      >{{ item.main.temp_min }}{{ units ? "°C" : "°F" }}</span
                    >
                  </div>
                  <div class="segment-item">
                    макс.
                    <span
                      >{{ item.main.temp_max }}{{ units ? "°C" : "°F" }}</span
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
<script>
import axios from "axios";
export default {
  props: {
    temp: {
      type: String,
    },
  },
  data() {
    return {
      apiKey: "6c9560d617d29b1453d471bbe38d365d",
      degNow: "0°C",
      wind: 0,
      humidity: 33,
      units: true,
      iconcode: "10d",
      currentWeatherTime: 13,
      dayWeather: [],
      fourDaysWeather: [],
      aWeek: [
        "Понедельник",
        "Вторник",
        "Среда",
        "Четверг",
        "Пятница",
        "Суббота",
        "Воскресенье",
      ],
    };
  },
  methods: {
    getDayWeather() {
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/forecast?lat=43.128373&lon=77.081641&appid=${this.apiKey}&units=metric`
        )
        .then((res) => {
          let start = res.data.list.indexOf(
            res.data.list.find(
              (el) => el.dt_txt.split(" ")[1].split(":")[0] == "00"
            )
          );
          this.dayWeather = [...res.data.list.slice(start, 15)];
        });
    },
    getData() {
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/forecast?lat=43.128373&lon=77.081641&appid=${
            this.apiKey
          }&units=${this.units ? "metric" : "imperial"}`
        ) // Latitude and longitude of shymbulak
        .then((response) => {
          this.getCurrentTime(response);
          let resMain;
          for (let i = 0; i < response.data.list.length; i++) {
            if (
              this.currentWeatherTime ==
              response.data.list[i].dt_txt.split(" ")[1].split(":")[0]
            ) {
              resMain = response.data.list[i];
            }
          }
          let temp = Math.floor(resMain.main.temp);
          this.degNow = temp += this.units ? "°C" : "°F";
          this.wind = resMain.wind.gust;
          this.humidity = resMain.main.humidity;
          this.iconcode = resMain.weather[0].icon;
          this.$emit("temp", {
            temp: this.degNow,
          });
        })
        .catch((err) => console.log(err));
    },
    getCurrentTime(response) {
      let timeNow = Number(new Date().toLocaleTimeString().split(":")[0]);
      let arrForTime = [];
      for (let i = 0; i < response.data.list.length; i++) {
        arrForTime.push(
          +response.data.list[i].dt_txt.split(" ")[1].split(":")[0]
        );
      }
      let closestLeft = Math.max(...arrForTime.filter((v) => v < timeNow));
      let closestRight = Math.min(...arrForTime.filter((v) => v > timeNow));
      if (closestRight - timeNow < timeNow - closestLeft) {
        this.currentWeatherTime = closestRight;
      } else {
        this.currentWeatherTime = closestLeft;
      }
    },
    log(event) {
      if (event.target.className.includes("two")) {
        document.querySelector(".day__container__wrapper").scrollBy(24, 0);
      } else {
        document.querySelector(".day__container__wrapper").scrollBy(-24, 0);
      }
    },
    getFourDaysWeather() {
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/forecast?lat=43.128373&lon=77.081641&appid=${
            this.apiKey
          }&${this.units ? "units=metric" : "units=imperial"}`
        )
        .then((res) => {
          this.fourDaysWeather = [
            ...res.data.list.filter(
              (el) => el.dt_txt.split(" ")[1].split(":")[0] == "15"
            ),
          ];
        });
    },
  },
  mounted() {
    this.getData();
    this.getDayWeather();
    this.getFourDaysWeather();
  },
};
</script>
<style lang="scss">
@import "../scss/main.scss";
</style>
