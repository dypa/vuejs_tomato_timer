<template>
    <div class="settings">
        timer: <input type="number" v-model.number="settings.timer" min="1" max="120"/>
        <br>
        pause: <input type="number" v-model.number="settings.pause" min="1" max="120"/>
        <br>
        rest:  <input type="number" v-model.number="settings.rest" min="1" max="120"/>
    </div>
</template>

<script>
export default {
  name: "Settings",
  props: ["settings"]
};
</script>

<style>
</style>
