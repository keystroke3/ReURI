<template>
    <div class="filearea">
        <span class="file-icon material-icons">{{ useFileIcon(fileType) }}</span>
        <div class="file-attributes">
            <table>
                <tr>
                    <td class="file-name">File Name: </td>
                    <td class="content"> {{ fileName }}</td>
                </tr>
                <tr>
                    <td class="file-size">File Size: </td>
                    <td> {{ formatBytes(fileSize) }}</td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script setup lang="ts">
import { useFileIcon } from '@/utils/Helpers';

useFileIcon

function formatBytes(bytes: number, decimals = 2) {
    if (!+bytes) return '0 Bytes'

    const k = 1024
    const dm = decimals < 0 ? 0 : decimals
    const sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']

    const i = Math.floor(Math.log(bytes) / Math.log(k))

    return `${parseFloat((bytes / Math.pow(k, i)).toFixed(dm))} ${sizes[i]}`
}

defineProps({
    filePath: {
        type: String,
        required: false
    },
    fileName: {
        type: String,
        required: true
    },
    fileType: {
        type: String,
        required: false
    },
    fileSize: {
        type: Number,
        required: true
    },
})


</script>

<style scoped>
table {
    table-layout: fixed;
    width: 30rem;
    /* margin: auto; */
    padding: 0 1rem;
}

.file-name {
    white-space: nowrap;
    width: 7rem;
}

.content {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}

.content:hover {
    overflow: visible;
    cursor: pointer;
}

.filearea {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    border: 2px solid var(--color-accent);
    border-radius: 15px;
    background-color: var(--color-element-bg);
    padding-bottom: 1rem;
}

.file-icon {
    font-size: clamp(9rem, 20vw, 12rem)
}

.file-attributes {
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.file-attributes a {
    color: var(--color-fg);
}
</style>