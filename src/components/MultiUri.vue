<script setup lang="ts">
import { ref, shallowRef } from 'vue';
import DiffOutput from './DiffOutput.vue';
let payload = ref('')
function uriDecode() {
}
function uriEncode() { }
</script>

<template>

  <form class="input-form" @submit.prevent="uriDecode">
    <textarea v-bind="payload" class="uri-input" type="url" name="uris" id="uris" placeholder="http://example.com
https://example2.com"></textarea>
    <label class="multi-label" for="uris">Enter a list of URIs each in its own line</label>
    <div class="form-btns">
      <button type="submit" @click.prevent="uriEncode" id="encode-btn">Decode</button>
      <button type="submit" @click.prevent="uriDecode" id="decode-btn">Encode</button>
    </div>
    <span class="char-count">{{
      payload.length + '/' + 5000
    }}</span>
    <Transition name="slide">
      <DiffOutput v-show="payload" />
    </Transition>
  </form>

</template>

<style scoped>
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

label {
  display: block;
}

form {
  width: inherit;
}


textarea {
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
  transition: all 4.4s ease;
}

.slide-leave-from,
.slide-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.slide-enter-from {
  opacity: 0;
  transform: translateY(-50px);
}


.slide-leave-to {
  opacity: 0;
  transform: translateY(50px);
}
</style>
