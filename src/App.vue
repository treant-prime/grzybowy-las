<script setup>
// import { RouterView } from 'vue-router'

import { ref, computed } from 'vue'
import comic1 from '@/assets/comic1.png'
import comic2 from '@/assets/comic2.png'

let comics = ref([
  {
    title: '01. ASP',
    imgUrl: comic1
  },
  {
    title: '02. Roboute Guilliman',
    imgUrl: comic2
  },
  {
    title: '03. Three',
    imgUrl: comic2
  }
])

const currentComic = ref(comics.value[0])

const previous = () => {
  const indexOfCurrentComic = comics.value.findIndex(
    (comic) => comic.title == currentComic.value.title
  )
  if (indexOfCurrentComic != -1 && indexOfCurrentComic != 0) {
    currentComic.value = comics.value[indexOfCurrentComic - 1]
  }
}

const next = () => {
  const indexOfCurrentComic = comics.value.findIndex(
    (comic) => comic.title == currentComic.value.title
  )
  if (indexOfCurrentComic != -1 && indexOfCurrentComic != comics.value.length - 1) {
    currentComic.value = comics.value[indexOfCurrentComic + 1]
  }
}

const isFirst = computed(() => {
  const indexOfCurrentComic = comics.value.findIndex(
    (comic) => comic.title == currentComic.value.title
  )
  return indexOfCurrentComic == 0
})

const isLast = computed(() => {
  const indexOfCurrentComic = comics.value.findIndex(
    (comic) => comic.title == currentComic.value.title
  )
  return indexOfCurrentComic == comics.value.length - 1
})
</script>

<template lang="pug">
.layout
  h1.site-header Grzybowy Las

  .button-bar
    div
      button(type="button" @click="previous" v-if="!isFirst") Poprzedni
    div
      button(type="button" @click="next" v-if="!isLast") Następny

  .comic-container
    .comic
      h1 {{ currentComic.title }}
      img(:src="currentComic.imgUrl")

</template>

<style scoped lang="scss">
.layout {
  width: 100%;
  margin: auto;
  padding: 0px 2rem;

  .site-header {
    text-align: center;
    margin-top: 2rem;
    margin-bottom: 2rem;
    font-size: 4rem;
    font-weight: bold;
  }

  .button-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem 0rem;
  }

  .comic-container {
    .comic {
      h1 {
        font-size: 2rem;
        font-weight: bold;
        margin-bottom: 1rem;
      }
      img {
        width: 100%;
      }
    }
  }
}

@media (min-width: 1024px) {
  .layout {
    width: 50%;
  }
}

// https://getcssscan.com/css-buttons-examples

button {
  background: #fff;
  backface-visibility: hidden;
  border-radius: 0.375rem;
  border-style: solid;
  border-width: 0.125rem;
  box-sizing: border-box;
  color: var(--vt-c-text-light-1);
  cursor: pointer;
  display: inline-block;
  font-family: Circular, Helvetica, sans-serif;
  font-size: 1.125rem;
  font-weight: 700;
  letter-spacing: -0.01em;
  line-height: 1.3;
  padding: 0.875rem 1.125rem;
  position: relative;
  text-align: left;
  text-decoration: none;
  transform: translateZ(0) scale(1);
  transition: transform 0.2s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

button:not(:disabled):hover {
  transform: scale(1.05);
}

button:not(:disabled):hover:active {
  transform: scale(1.05) translateY(0.125rem);
}

button:focus {
  outline: 0 solid transparent;
}

button:focus:before {
  content: '';
  left: calc(-1 * 0.375rem);
  pointer-events: none;
  position: absolute;
  top: calc(-1 * 0.375rem);
  transition: border-radius;
  user-select: none;
}

button:focus:not(:focus-visible) {
  outline: 0 solid transparent;
}

button:focus:not(:focus-visible):before {
  border-width: 0;
}

button:not(:disabled):active {
  transform: translateY(0.125rem);
}
</style>
