<template>
  <div id="app">
    <md-card class="card-display">
      <div class="head-display">
        <md-field>
          <label>Time in seconds</label>
          <md-input v-model="seconds"></md-input>
        </md-field>
      </div>
      <p>{{time}}</p>
      <div class="md-layout md-alignment-center-center md-layout-nowrap">
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(1)">1</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(2)">2</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(3)">3</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(4)">4</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(5)">5</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(6)">6</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(7)">7</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(8)">8</md-button></div>
        <div class="md-layout-item md-xsmall-size-33 md-small-size-33 md-medium-size-33 md-large-size-33 md-xlarge-size-33"><md-button class="md-raised btn-number" @click="tail(9)">9</md-button></div>
        <div class="md-layout-item md-xsmall-size-50 md-small-size-50 md-medium-size-50 md-large-size-50 md-xlarge-size-50"><md-button class="md-raised btn-number" @click="tail(0)">0</md-button></div>
        <div class="md-layout-item md-xsmall-size-50 md-small-size-50 md-medium-size-50 md-large-size-50 md-xlarge-size-50"><md-button class="md-raised btn-option" @click="clear()">C</md-button></div>
      </div>
    </md-card>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import moment from 'moment';

@Component
export default class App extends Vue {
  public seconds = '0';
  get time(): string {
    let strsec = this.seconds;
    strsec = strsec.replace(',', '.');
    strsec = strsec.replace(/[^e\.\d]+/g, '');
    const seconds = parseFloat(strsec) || 0;
    this.seconds = seconds.toString();
    const duration = moment.duration(seconds, 'seconds');
    let time = '';
    if (duration.seconds()) {
      time = `${duration.seconds()}s`;
      console.log(duration.seconds());
    }
    if (duration.minutes()) {
      time = `${duration.minutes()}m${duration.seconds()}s`;
      console.log(duration.minutes());
    }
    if (duration.hours() ) {
      time = `${duration.hours()}h${duration.minutes()}m${duration.seconds()}s`;
      console.log(duration.hours());
    }
    if (duration.days()) {
      time = `${duration.days()}d${duration.hours()}h${duration.minutes()}m${duration.seconds()}s`;
      console.log(duration.days());
    }
    if (duration.weeks()) {
      time = `${duration.weeks()}w${duration.days()}d${duration.hours()}h${duration.minutes()}m${duration.seconds()}s`;
      console.log(duration.weeks());
    }
    if (duration.months()) {
      time = `${duration.months()}M${duration.weeks()}w${duration.days()}d${duration.hours()}h${duration.minutes()}
        m${duration.seconds()}s`;
      console.log(duration.months());
    }
    if (duration.years()) {
      time = `${duration.years()}Y${duration.months()}M${duration.weeks()}w${duration.days()}d${duration.hours()}
        h${duration.minutes()}m${duration.seconds()}s`;
      console.log(duration.years());
    }
    return time;
  }

  public tail(a: number) {
    let seconds = parseFloat(this.seconds);
    seconds *= 10;
    seconds += a;
    this.seconds = seconds.toString();
  }

  public clear() {
    this.seconds = '0';
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}
.btn-option {
  background-color: #c4d8ff !important;
}
.btn-number {
  background-color: #e9e9e9 !important;
}
.md-button.md-raised.md-theme-default {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 75px;
}
.head-display {
  padding-top: 30px;
  margin-right: 30px;
  margin-left: 30px;
}
.card-display {
  margin-left: auto;
  margin-right: auto;
  width: 100%;
}
@media (max-width: 1279px) {
  #app {
    margin: 0;
  }
  .md-button.md-raised.md-theme-default {
    padding: 20px;
  }
}
@media (min-width: 1280px) {
  #app {
    margin: 2% 30%;
  }
  .md-button.md-raised.md-theme-default {
    padding: 75px;
  }
}
</style>
