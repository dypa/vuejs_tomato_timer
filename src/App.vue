<template>
  <div id="app">
    <button class="tab-button" v-on:click="activeComponent = 'timer'" v-bind:class="['tab-button', { active: activeComponent === 'timer' }]">Timer</button>
    <button class="tab-button" v-on:click="activeComponent = 'settings'" v-bind:class="['tab-button', { active: activeComponent === 'settings' }]">Settings</button>
    
    <component v-bind:is="currentTabComponent" v-bind:settings.sync="settings" class="tab"></component>
  </div>
</template>

<script>
import Timer from "./components/Timer.vue";
import Settings from "./components/Settings.vue";

export default {
  name: "app",
  components: {
    Settings,
    Timer
  },
  data: function() {
    return {
      activeComponent: "timer",
      settings: {
        timer: 25,
        pause: 5,
        rest: 15
      }
    };
  },
  computed: {
    currentTabComponent: function() {
      let str = this.activeComponent;
      return str[0].toUpperCase() + str.slice(1).toLowerCase();
    }
  }
};
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.tab-button {
  padding: 6px 10px;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
  border: 1px solid #ccc;
  cursor: pointer;
  background: #f0f0f0;
  margin-bottom: -1px;
  margin-right: -1px;
}
.tab-button:hover {
  background: #e0e0e0;
}
.tab-button.active {
  background: #e0e0e0;
}
.tab {
  border: 1px solid #ccc;
  padding: 10px;
}
</style>
