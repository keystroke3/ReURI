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
  <div class="content">
    <h1>Welcome to ReUri</h1>
    <h2>Encode and decode URIs</h2>
    <div class="tabs">
      <button @click="tab = 'URI'" class="tab single" :class="{ 'active-tab': tab === 'URI' }">Single</button>
      <button @click="tab = 'URIs'" class="tab multi" :class="{ 'active-tab': tab === 'URIs' }">Multiple</button>
      <button @click="tab = 'File'" class="tab file" :class="{ 'active-tab': tab === 'File' }">File</button>
    </div>
    <input v-show="tab === 'URI'" type="text" class="uri-input single-url-input" placeholder="http://example.com">
    <form v-show="tab === 'URIs'" class="input-form" @submit.prevent="uriDecode">
      <textarea class="uri-input" type="url" name="uris" id="uris" placeholder="http://example.com
https://example2.com"></textarea>
      <label class="multi-label" for="uris">Enter a list of URIs each in its own line</label>
    </form>
    <FileInput v-show="tab === 'File'" />
    <div class="form-btns">
      <button v-show="tab !== 'URI'" type="submit" @click.prevent="uriEncode" id="encode-btn">Decode</button>
      <button v-show="tab !== 'URI'" type="submit" @click.prevent="uriDecode" id="decode-btn">Encode</button>
    </div>
  </div>
</template>

<style scoped>
.content {
  width: min(95vw, 70rem);
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
  margin-block: 5rem 0.5rem;
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
  transition: border-color 0.25s;
}

button:hover {
  border-color: var(--color-green);
}

button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}
</style>
