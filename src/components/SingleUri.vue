<script setup lang="ts">

import { ref, watch } from 'vue';
const inputUri = ref('')
const outputUri = ref('')
const inputError = ref(false)
const mode = ref('decode')
function convert() {
  outputUri.value = mode.value === 'encode' ? encodeURIComponent(inputUri.value) : decodeURIComponent(inputUri.value)
}

watch(inputUri, (inputUri, prev) => {
  convert()
})
watch(mode, (mode, prev) => {
  convert()
})
</script>

<template>
  <div class="simple-input">
    <div class="modes">
      <label class="mode" :class="{ 'active-mode': mode === 'decode' }">
        <input type="radio" v-model="mode" name="active-tab" id="multi" value="decode"> Decode
      </label>
      <label class="mode" :class="{ 'active-mode': mode === 'encode' }">
        <input type="radio" v-model="mode" name="active-tab" id="single" value='encode' /> Encode
      </label>
    </div>

    <input autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" class="url-input frost"
      v-model="inputUri" type="text" :class="{ 'input-error': inputError }"
      :placeholder="mode === 'encode' ? 'http://example.com' : 'https%3A%2F%2Fexample.com'">

    <Transition name="drop">
      <p v-show="inputUri" class="frost">
        <a target="_blank" :href="outputUri">{{ outputUri }}</a>
      </p>
    </Transition>
  </div>
</template>

<style scoped lang="scss">
.simple-input {
  width: inherit;
  margin-top: 3rem;
}

.modes {
  margin-top: 1rem;
}

.mode input {
  display: none;
}

.mode {
  flex-basis: 100%;
  text-align: center;
  padding: 0.5rem;
  font-size: 1.1rem;
  border-radius: 0;
  border-bottom: 2px solid transparent;
  background-color: var(--color-element-bg);
  color: var(--color-fg);
  cursor: pointer;
  border: 2px solid transparent;
  transition: all 0.5s ease;

  &:hover {
    border-color: var(--color-green);
  }

  &:first-child {
    border-radius: 10px 0 0 10px;
  }

  &:last-child {
    border-radius: 0 10px 10px 0;
  }
}




.active-mode {
  background-color: var(--color-green);
  color: var(--color-bg);
  border-bottom: 2px solid var(--color-green);
}


p {
  font: 1.4rem monospace;
  color: var(--color-green);
  width: inherit;
  background-color: var(--color-element-bg);
  padding: 1rem;
  overflow-x: auto;
  border-radius: 10px;

  a {
    color: var(--color-green);
    text-decoration: underline;
  }
}

.url-input {
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
  height: 4rem;
  overflow-y: auto;
  margin-bottom: 1rem;
  margin-top: 2rem;
  text-align: center;
}
</style>
