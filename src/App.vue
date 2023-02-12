<script setup lang="ts">
import { ref, shallowRef } from 'vue';
import FileInput from './components/FileInput.vue'
import DiffOutput from './components/DiffOutput.vue'
import SingleUri from './components/SingleUri.vue';
import MultiUri from './components/MultiUri.vue';

const tab = ref('URI')
const activeInput = shallowRef(SingleUri)


function uriDecode() {
}
function uriEncode() {
}
</script>

<template>
  <div class="payload-input">
    <h1>Welcome to ReUri</h1>
    <h2>Encode and decode URIs</h2>
    <div class="tabs">
      <label class="tab" :class="{ 'active-tab': activeInput === SingleUri }">Single
        <input type="radio" v-model="activeInput" name="active-tab" id="single" :value="SingleUri" />
      </label>
      <label class="tab" :class="{ 'active-tab': activeInput === MultiUri }">Multiple
        <input type="radio" v-model="activeInput" name="active-tab" id="multi" :value="MultiUri">
      </label>
      <label class="tab" :class="{ 'active-tab': activeInput === FileInput }">File
        <input type="radio" v-model="activeInput" name="active-tab" id="file" :value="FileInput" />
      </label>
    </div>
    <Transition mode="out-in" name="slide">
      <component :is="activeInput"></component>
    </Transition>


  </div>
</template>

<style scoped>
.payload-input {
  width: min(95vw, 90rem);
  margin: 0 auto;
  text-align: center;
}

.tabs {
  display: flex;
  width: inherit;
  margin-bottom: 1rem;
}

.tab {
  flex-basis: 100%;
  text-align: center;
  padding: 1rem;
  font-size: 1.2rem;
  border-radius: 0;
  border-bottom: 2px solid transparent;
  background-color: var(--color-element-bg);
  color: var(--color-fg);
  cursor: pointer;
}

.tab input {
  display: none;
}

.tab-inputs {
  width: inherit;
}

.tab:first-child {
  border-radius: 10px 0 0 10px;
  border-right: 1px solid var(--color-green);
}

.tab:last-child {
  border-radius: 0 10px 10px 0;
  border-left: 1px solid var(--color-green);
}

.active-tab {
  background-color: var(--color-green);
  color: var(--color-bg);
  border-bottom: 2px solid var(--color-green);
}

.tab-input {
  display: none;
}

.form-btns {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-top: 1rem;
  place-content: center;
}

.multi-label {
  font-size: 1.2rem;
}

h1 {
  font-size: clamp(2.3rem, 4.5vw, 4rem);
  line-height: 1.1;
  margin-block: 3rem 0.5rem;
}

h2 {
  font-size: clamp(1.3rem, 1.9vw, 2.1rem);
  line-height: 1.1;
  margin-block: 0 2rem
}

label {
  display: block;
}

form {
  width: inherit;
}


.uri-input {
  border: 4px solid var(--color-green);
  border-bottom: 0;
  border-top: 0;
  border-radius: 10px;
  background-color: var(--color-element-bg);
  color: var(--color-fg);
  font-family: monospace;
  font-size: 1.0rem;
  padding: 1.1rem;
  outline: transparent;
  width: inherit;
  height: 12rem;
  overflow-y: auto;
  margin-bottom: 1rem;

}


.single-url-input {
  margin-top: 5%;
  height: 4rem;
  text-align: center;
}

button {
  border-radius: 10px;
  border: 1px solid transparent;
  padding: 0.6em 1.2rem;
  font-size: 1.3rem;
  font-weight: 500;
  font-family: inherit;
  background-color: var(--color-green);
  color: var(--color-bg);
  cursor: pointer;
  Transition: border-color 0.25s;
}

button:hover {
  border-color: var(--color-green);
}

button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

.slide-leave-active,
.slide-enter-active {
  transition: all 0.4s ease;
}

.slide-leave-from,
.slide-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(-50px);
}


.slide-leave-to {
  opacity: 0;
  transform: translateX(50px);
}

.fade-in-leave-to,
.fade-in-enter-from {
  opacity: 0;
  transform: translateY(-20px);
}

.fade-in-leave-from,
.fade-in-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.fade-in-leave-active,
.fade-in-enter-active {
  transition: all 1.6s ease
}

.fade-in-enter-active {
  transition: all 1.6s ease
}
</style>
