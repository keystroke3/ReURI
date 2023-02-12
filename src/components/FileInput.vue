<template >
    <div>
        <form>
            <div @dragenter.prevent="toggleActive" @dragleave.prevent="toggleActive" @dragover.prevent
                @drop.prevent="handleDrop" class="dropzone"
                :class="{ 'active-dropzone': active, 'file-selected': file.fileName }">
                <span name="Selected File" class="file-name" v-show="file.fileName">{{ file.fileName }}</span>
                <span name="Select File" v-show="!file.fileName">Drag and Drop</span>
                <span v-show="!file.fileName">Or</span>
                <label class="file-chooser" for="selectFile">{{ chooserLabel() }}</label>
                <input type="file" accept="text/*" name="Upload" id="selectFile" @change="handleChange">
            </div>
        </form>

    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
const active = ref(false)
function toggleActive() {
    active.value = !active.value
}
const defaultFile = {
    fileName: '',
    fileType: '',
}
let file = ref(defaultFile)

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
</style>
