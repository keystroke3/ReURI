<template >
    <div class="results">
        <div class="diff original">
            <label for="original">Original</label>
            <textarea name="original-urls" id="original">Lorem ipsum dolor sit amet consectetur adipisicing elit. Animi, pariatur sint omnis minima temporibus velit consectetur modi optio perferendis repellat dolor tempora similique ad totam voluptatibus quibusdam earum corrupti cumque!
        </textarea>
        </div>
        <div class="diff converted">
            <label for="converted">Converted</label>
            <textarea name="converted-urls" id="converted">Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum qui ratione laudantium fuga expedita dignissimos, ab adipisci nobis! Nesciunt doloribus, aliquam nulla sit officiis in? Distinctio explicabo dolore qui exercitationem!
        </textarea>
        </div>
    </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
.results {
    display: flex;
    /* flex-wrap: wrap; */
    width: inherit;
    gap: 2rem;
    margin-top: 2%;
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
}
</style>
