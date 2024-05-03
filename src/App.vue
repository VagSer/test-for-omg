<script setup>
import { onMounted, ref } from 'vue';
import AppList from './components/AppList.vue';

const myList = ref([])
const firstVisibleElementIndex = ref(0)
const lastVisibleElementIndex = ref(9)

const generateRandomInteger = (min, max) => Math.floor(Math.random() * (max - min + 1) + min)

const isVisible = (el) => {
  let rect = el.getBoundingClientRect();
    return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
        rect.right <= (window.innerWidth || document.documentElement.clientWidth)
    );
}

const debounce = (func, delay) => {
  let timeoutId
  return function() {
    const context = this
    const args = arguments
    clearTimeout(timeoutId)
    timeoutId = setTimeout(() => func.apply(context, args), delay)
  };
};

const updateBothIndexes = debounce(() => {
  let elements = [...document.querySelectorAll('.appListItem')]
  elements = elements.filter(element => isVisible(element) === true)
  firstVisibleElementIndex.value = elements.at(0).id
  lastVisibleElementIndex.value = elements.at(-1).id
  console.log('Отработала')
}, 1000);

const generateList = async () => {
  let howMany = generateRandomInteger(100, 150)
  let index = 0
  while (myList.value.length < howMany) {
    let newElement = []
    let howManyNewElement = generateRandomInteger(11, 20)
    for (let i = 0; i <= howManyNewElement; i++) {
      newElement.push(generateRandomInteger(10, 99))
    }
    myList.value.push({index, list: [...newElement]})
    index++
  }
}

const updateRandomVisibleNumber = () => {
  let randomElement = generateRandomInteger(+firstVisibleElementIndex.value, +lastVisibleElementIndex.value)
  let randomItem = generateRandomInteger(0, (myList.value.at(randomElement).list.length - 1))
  myList.value[randomElement].list[randomItem] = generateRandomInteger(-99, -10)
}

onMounted(() => {
  generateList()
  document.addEventListener('scroll', () => updateBothIndexes(), { passive: true })
  setInterval(() => {
    updateRandomVisibleNumber()
  }, 1000)
})
</script>

<template>
  <h1>My app</h1>
  <AppList :list="myList" />
</template>

<style scoped>
</style>
