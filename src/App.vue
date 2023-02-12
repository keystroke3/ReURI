<script setup lang="ts">
import { ref } from 'vue';
import FileInput from './components/FileInput.vue'

var tab = ref('URI')
function uriDecode() {
}
function uriEncode() {
}
</script>

<template>
  <h1>Welcome to ReUri</h1>
  <h2>A simple tool to help encode and decode URIs</h2>
  <div class="tabs">
    <!-- <div class="tab single" :class="{ 'active-tab': !multi }">
      <label for="single-url" class="tab-label">Single URI</label>
      <input @click="multi = false" class="tab-input" type="radio" name="change-tab" id="single-url" checked />
    </div> -->
    <!-- <div class="tab multi" :class="{ 'active-tab': multi }">
      <label for="multi-url" class="tab-label" :class="{ 'active-tab': multi }">Multiple URIs</label>
      <input @click="multi = true" class="tab-input" type="radio" name="change-tab" id="multi-url">
    </div> -->

    <button @click="tab = 'URI'" class="tab single" :class="{ 'active-tab': tab === 'URI' }">Single</button>
    <button @click="tab = 'URIs'" class="tab multi" :class="{ 'active-tab': tab === 'URIs' }">Multiple</button>
    <button @click="tab = 'File'" class="tab multi" :class="{ 'active-tab': tab === 'File' }">From File</button>
  </div>
  <input v-show="tab === 'URI'" type="text" class="uri-input single-url-input" placeholder="http://example.com">
  <form v-show="tab === 'URIs'" class="input-form" @submit.prevent="uriDecode">
    <textarea class="uri-input" type="url" name="uris" id="uris" placeholder="http://example.com
https://example2.com"></textarea>
    <label for="uris">Enter a list of URIs each in its own line</label>
    <div class="form-btns">
      <button type="submit" @click.prevent="uriEncode" id="encode-btn">Decode</button>
      <button type="submit" @click.prevent="uriDecode" id="decode-btn">Encode</button>
    </div>
  </form>
  <FileInput />
</template>

<style scoped>
.tabs {
  display: flex;
  width: 62.9vw;
  margin: auto;
  margin-bottom: 1rem;
}

.tab {
  width: 25vw;
  text-align: center;
  padding: 1rem;
  font-size: 1.2rem;
  border-radius: 15px;
  background-color: var(--color-element-bg);
  margin: auto;
}

.active-tab {
  background-color: var(--color-green);
  color: var(--color-bg);
}

.tab-input {
  display: none;
}


h1 {
  font-size: 3.2em;
  line-height: 1.1;
}

label {
  display: block;
}

.uri-input {
  border: 4px solid var(--color-green);
  border-bottom: 0;
  border-top: 0;
  border-radius: 10px;
  background-color: var(--color-element-bg);
  font-family: monospace;
  font-size: 1.0rem;
  padding: 1.1rem;
  outline: transparent;
  width: 60vw;
  height: 22rem;
  overflow-y: scroll;
  margin-bottom: 1rem;
}

.single-url-input {
  height: 2rem;
  text-align: center;
}

button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2rem;
  font-size: 1.3rem;
  font-weight: 500;
  font-family: inherit;
  background-color: var(--color-green);
  cursor: pointer;
  transition: border-color 0.25s;
}

button:hover {
  border-color: var(--color-green);
}

button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

.form-btns {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin: auto;
  place-content: center;
}
</style>
