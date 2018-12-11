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

@Component
export default class App extends Vue {
  public seconds = '0';
  get time(): string {
    let strsec = this.seconds;
    strsec = strsec.replace(',', '.');
    strsec = strsec.replace(/[^e\.\d]+/g, '');
    let seconds = parseFloat(strsec) || 0;
    this.seconds = seconds.toString();
    let minutes = 0;
    let hours = 0;
    let days = 0;
    let weeks = 0;
    let months = 0;
    let years = 0;
    if (!seconds) return '0s';
    let time = `${seconds}s`;
    if (seconds > 59) {
      minutes = Math.floor(seconds / 60);
      seconds -= minutes * 60;
      time = `${minutes}m${seconds}s`;
    }
    if (minutes && minutes > 59) {
      hours = Math.floor(minutes / 60);
      minutes -= hours * 60;
      time = `${hours}h${minutes}m${seconds}s`;
    }
    if (hours && hours > 23) {
      days = Math.floor(hours / 24);
      hours -= days * 24;
      time = `${days}d${hours}h${minutes}m${seconds}s`;
    }
    if (days && days > 6) {
      weeks = Math.floor(days / 7);
      days -= weeks * 7;
      time = `${weeks}w${days}d${hours}h${minutes}m${seconds}s`;
    }
    if (weeks && weeks > 3) {
      months = Math.floor(weeks / 4);
      weeks -= months * 4;
      time = `${months}M${weeks}w${days}d${hours}h${minutes}m${seconds}s`;
    }
    if (months && months > 11) {
      years = Math.floor(months / 12);
      months -= years * 12;
      time = `${years}y${months}M${weeks}w${days}d${hours}h${minutes}m${seconds}s`;
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
