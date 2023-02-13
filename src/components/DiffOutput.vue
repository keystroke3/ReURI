<template >
    <div class="results">
        <div class="diff original">
            <label for="original">Original</label>
            <textarea autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" class="frost"
                name="original-urls" id="original">{{ originalValue }}</textarea>
        </div>
        <div class="diff converted">
            <label for="converted">{{ props.mode === 'encode' ? 'Encoded' : 'Decoded' }}</label>
            <textarea autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" class="frost"
                name="converted-urls" id="converted">{{ convertedValue }}</textarea>
        </div>
    </div>
</template>

<script setup lang="ts">

const props = defineProps({
    mode: {
        type: String,
        default: 'encode',
    },
    convertedValue: {
        type: String
    },
    originalValue: {
        type: String
    }

})

</script>

<style scoped lang="scss">
.results {
    display: flex;
    width: inherit;
    gap: 2rem;
    margin-top: 2%;
    margin-bottom: 5%;
    flex-wrap: wrap;
}

.diff {
    width: inherit;
    display: flex;
    flex-direction: column;
    flex: 1;
    min-width: min(100%, 22rem);

}

label {
    display: block;
    background-color: var(--color-green);
    color: var(--color-bg);
    border-radius: 10px 10px 0 0;
    font-size: 1.2rem;
    padding: 0.5rem 0;
}

textarea {
    border: 0;
    border-bottom: 4px solid var(--color-green);
    border-radius: 0 0 10px 10px;
    background-color: var(--color-element-bg);
    color: var(--color-fg);
    overflow: auto;
    height: 20rem;
    padding: 1rem;
    font-size: 1.1rem;
}
</style>
