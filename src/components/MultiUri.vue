<script setup lang="ts">
import { ref } from 'vue';
import DiffOutput from './DiffOutput.vue';

const inputUris = ref('')
const expandedInput = ref('')
const converted = ref('')
const inputError = ref(false)
const mode = ref('')

function convert(action: string) {
  if (!inputUris.value) {
    inputError.value = true
    setTimeout(() => {
      inputError.value = false
    }, 2000)
  }
  const uris = inputUris.value.split('\n')
  converted.value = uris.map((uri) => {
    return action === 'decode' ? decodeURIComponent(uri) : encodeURIComponent(uri)
  }).join('\n\n')
  expandedInput.value = uris.join('\n\n')
  mode.value = action
}
</script>

<template>
  <div class="multi-uri">
    <form class="input-form" @submit.prevent="convert('encode')">
      <textarea v-model="inputUris" class="uri-input frost" type="url" name="uris" id="uris" placeholder="http://example.com
https://example2.com"></textarea>
      <label class="multi-label" for="uris">Enter a list of URIs each in its own line</label>
      <div class="form-btns">
        <button type="submit" @click.prevent="convert('decode')" id="encode-btn">Decode</button>
        <button type="submit" @click.prevent="convert('encode')" id="decode-btn">Encode</button>
      </div>
    </form>
    <Transition name="drop">
      <DiffOutput v-show="mode" :mode="mode" :original-value="expandedInput" :converted-value="converted" />
    </Transition>
  </div>
</template>

<style scoped lang="scss">
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

.multi-uri {
  width: inherit;
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
  transition: border-color 0.25s;

  &:hover {
    border-color: var(--color-green);
    background-color: var(--color-blue);
    color: var(--color-fg);
    transition: all 0.5s ease;
  }

  &:focus,
  &:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
  }
}
</style>
