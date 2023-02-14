<script setup lang="ts">
import { ref, shallowRef, watch } from 'vue';
import FileInput from './components/FileInput.vue'
import SingleUri from './components/SingleUri.vue';
import MultiUri from './components/MultiUri.vue';

const activeTab = shallowRef(SingleUri)
const animation = ref('slide-leftwards')

watch(activeTab, (from, to) => {
  const seek = from.__name! + to.__name
  switch (seek) {
    case 'SingleUriMultiUri':
      animation.value = 'slide-rightwards'
      break;
    case 'MultiUriFileInput':
      animation.value = 'slide-rightwards'
      break;
    case 'FileInputMultiUri':
      animation.value = 'slide-leftwards'
      break;
    case 'MultiUriSingleUri':
      animation.value = 'slide-leftwards'
      break;
    case 'SingleUriFileInput':
      animation.value = 'slide-rightwards'
      break;
    default:
      animation.value = 'slide-leftwards'
      break;
  }
})

</script>

<template>
  <div class="main">
    <div class="content">
      <h1>Welcome to ReURI</h1>
      <h2>Quickly encode and decode URIs</h2>
      <div class="tabs">
        <label class="tab" :class="{ 'active-tab': activeTab === SingleUri }">Single
          <input type="radio" v-model="activeTab" name="active-tab" id="single" :value="SingleUri" />
        </label>
        <label class="tab" :class="{ 'active-tab': activeTab === MultiUri }">Multiple
          <input type="radio" v-model="activeTab" name="active-tab" id="multi" :value="MultiUri">
        </label>
        <label class="tab" :class="{ 'active-tab': activeTab === FileInput }">File
          <input type="radio" v-model="activeTab" name="active-tab" id="file" :value="FileInput" />
        </label>
      </div>
      <transition appear mode="out-in" :name="animation">
        <component :is="activeTab"></component>
      </transition>

      <ul class="circles">
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </div>
    <footer>
      <ul>
        <li>
          Github:
          <a href="http://github.com/keystroke3" target="_blank" rel="noopener noreferrer">keystroke3</a>
        </li>
        <li>
          Twitter:
          <a href="http://twitter.com/keystroke_3" target="_blank" rel="noopener noreferrer">keystroke_3</a>
        </li>
        <li>
          Email:
          <a href="mailto:keystroke33@gmail.com">keystroke33@gmail.com</a>
        </li>
      </ul>
      <p>© {{ new Date().getFullYear() }}</p>
    </footer>
  </div>

</template>

<style scoped lang="scss">
/* Background animation
CREDIT: Mohammad Abdul Mohaiman
SOURCE: https://codepen.io/mohaiman/pen/MQqMyo 
*/

.circles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: -1;
}

.circles li {
  position: absolute;
  display: block;
  list-style: none;
  width: 20px;
  height: 20px;
  background: rgba(255, 255, 255, 0.2);
  animation: animate 25s linear infinite;
  bottom: -150px;

}

.circles li:nth-child(1) {
  left: 25%;
  width: 80px;
  height: 80px;
  animation-delay: 0s;
}


.circles li:nth-child(2) {
  left: 10%;
  width: 20px;
  height: 20px;
  animation-delay: 2s;
  animation-duration: 12s;
}

.circles li:nth-child(3) {
  left: 70%;
  width: 20px;
  height: 20px;
  animation-delay: 4s;
}

.circles li:nth-child(4) {
  left: 40%;
  width: 60px;
  height: 60px;
  animation-delay: 0s;
  animation-duration: 18s;
}

.circles li:nth-child(5) {
  left: 65%;
  width: 20px;
  height: 20px;
  animation-delay: 0s;
}

.circles li:nth-child(6) {
  left: 75%;
  width: 110px;
  height: 110px;
  animation-delay: 3s;
}

.circles li:nth-child(7) {
  left: 35%;
  width: 150px;
  height: 150px;
  animation-delay: 7s;
}

.circles li:nth-child(8) {
  left: 50%;
  width: 25px;
  height: 25px;
  animation-delay: 15s;
  animation-duration: 45s;
}

@keyframes animate {

  0% {
    transform: translateY(0) rotate(0deg);
    opacity: 1;
    border-radius: 0;
  }

  100% {
    transform: translateY(-1000px) rotate(720deg);
    opacity: 0;
    border-radius: 50%;
  }

}

/* END BACKGROUND ANIMATION CREDIT */



.main {
  height: 100vh;
  position: relative;
}

.content {
  text-align: center;
  width: min(95vw, 90rem);
  margin: 0 auto;
  height: 100%;
}

footer {
  height: 5rem;
  flex-shrink: 0;
  background-color: #ffffff24;
  padding: 1rem;
  align-items: center;
  text-align: center;
  position: absolute;
  bottom: 0;
  width: 100%;


  ul {
    list-style: none;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    column-gap: 1rem;
  }

  li {
    font-size: 1.2rem;
  }
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
  border-bottom: 5px solid transparent;
  background-color: var(--color-element-bg);
  color: var(--color-fg);
  cursor: pointer;

  &:hover {
    border-bottom: 5px solid var(--color-green);
  }

  input {
    display: none;
  }

  transition: all 0.5s ease;

  &:first-child {
    border-radius: 10px 0 0 10px;
    border-right: 1px solid var(--color-green);
  }

  &:last-child {
    border-radius: 0 10px 10px 0;
    border-left: 1px solid var(--color-green);
  }

}

.active-tab {
  background-color: var(--color-green);
  color: var(--color-bg);
  border-bottom: 2px solid var(--color-green);
  transition: background-color 1s ease;

  &:hover {
    background-color: var(--color-green);
  }
}

h1 {
  font-size: clamp(2.3rem, 4.5vw, 4rem);
  line-height: 1.1;
  padding-top: 3rem;
  margin-bottom: 0.5rem;
  font-weight: 100;
}

h2 {
  font-size: clamp(1.3rem, 1.9vw, 2.1rem);
  line-height: 1.1;
  margin-bottom: 7rem;
}

label {
  display: block;
}

form {
  width: inherit;
}

a {
  color: var(--color-green);
  text-decoration: underline;
  text-shadow: 0 0 5px 1px var(--color-green);
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

  &::hover {
    border-color: var(--color-green);
  }

}
</style>
