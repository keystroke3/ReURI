<template >
    <div>
        <form v-if="ready">
            <div @dragenter.prevent="toggleActive" @dragleave.prevent="toggleActive" @dragover.prevent
                @drop.prevent="handleDrop" class="dropzone"
                :class="{ 'active-dropzone': active, 'file-selected': file.fileName }">
                <span name="Selected File" class="file-name" v-show="file.fileName">{{ file.fileName }}</span>
                <span name="Select File" v-show="!file.fileName">Drag and Drop</span>
                <span v-show="!file.fileName">Or</span>
                <label class="file-chooser" for="selectFile">{{ chooserLabel() }}</label>
                <input type="file" accept="text/*" name="Upload" id="selectFile" @change="handleChange">
            </div>
            <Transition name="slide">
                <div class="form-btns">
                    <button type="submit" @click.prevent="uriEncode" id="encode-btn">Decode</button>
                    <button type="submit" @click.prevent="uriDecode" id="decode-btn">Encode</button>
                </div>
            </Transition>
        </form>
        <h1 v-if="!ready"> Coming Soon ... </h1>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
const active = ref(false)
const ready = ref(false)
function toggleActive() {
    active.value = !active.value
}
const defaultFile = {
    fileName: '',
    fileType: '',
}
let file = ref(defaultFile)
function uriEncode() { }
function uriDecode() { }
function chooserLabel() {
    if (file.value.fileName) {
        return "Select Different File"
    }
    return "Select File"
}

function handleChange(e: Event): void {
    const el = e.target as HTMLInputElement;
    file.value = {
        fileName: el.files![0].name,
        fileType: el.files![0].type,
    }
}
function handleDrop(e: DragEvent) {
    toggleActive()
}


</script>

<style scoped>
.dropzone {
    width: inherit;
    border: 4px solid var(--color-green);
    border-top: 0;
    border-bottom: 0;
    border-radius: 10px;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: var(--color-element-bg);
    transition: 200ms ease all;
    row-gap: 0.5rem;
    height: 12rem;
}


.active-dropzone {
    border-style: dotted;
}

.file-selected {
    border-style: solid;
}

.file-chooser {
    background-color: var(--color-green);
    color: var(--color-bg);
    padding: 1rem;
    border-radius: 10px;
    cursor: pointer;
}

.file-name {
    width: min(60vw, 40rem);
    padding: 1rem;
    overflow-x: auto;
}

.form-btns {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin-top: 1rem;
    place-content: center;
}

h1 {
    font-size: clamp(2.3rem, 4.5vw, 4rem);
    line-height: 1.1;
    padding-top: 3rem;
    margin-bottom: 0.5rem;
    font-weight: 100;
}

label {
    font-size: 1.2rem;
}

input {
    display: none;
}

form {
    display: flex;
    flex-direction: column;
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
    transition: border-color 0.25s;
    cursor: pointer;
}

button:hover {
    border-color: var(--color-green);
}

button:focus,
button:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
}
</style>
