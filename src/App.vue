<template>
  <div class="container">
    <h1>Custom DropDown</h1>
    <div class="dropdown" ref="dropdown">
      <div class="select" @click="view">
        <!-- <span class="selected" v-if="chevron = true" v-for="manyItem in manyItemSelected">{{ manyItem }}</span> -->
        <span class="selected">{{ selectedText }}</span>
        <!-- <span class="selected" v-else v-for="manyItem in manyItemSelected">{{ manyItem }}</span> -->
        <div class="caret" :class="{ 'caret_rotate': isOpen }"></div>
      </div>
      <ul :class="{ 'menu_open': isOpen }">
        <li class="option_section" @click="displayChev">
          <div class="chev" v-show="chevron"><img src="/src/assets/check_small_24dp_000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="width: 20px;" /></div>
          <option>Select many item</option>
        </li>
        <li
          v-for="(item, index) in items"
          :key="index"
          @click="selectItem(item, index)">
          <span>{{ item }}</span>
          <div :class="['div', { 'display_button': selectedIndex === index }]">
            <img src="/src/assets/sma.png" alt="" style="width: 25px;" />
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const isOpen = ref(false);
const selectedText = ref('Select an item');
const items = ['First Item', 'Second Item', 'Third Item', 'Fourth Item', 'Fifth Item'];
const selectedIndex = ref(1); 
const chevron = ref(false);
const manyItemSelected = ref([])
function view() {
  isOpen.value = !isOpen.value;
}

function selectItem(item: string, index: number) {
  selectedText.value = item;
  isOpen.value = false;
  selectedIndex.value = index;  
  manyItemSelected.value.push(item)
}


const displayChev = () => {
  chevron.value = !chevron.value;
};
</script>

<style scoped>
.container {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  padding-top: 40px;
  flex-direction: column;
}

.dropdown {
  width: 250px;
}

.dropdown * {
  box-sizing: border-box;
}

.select {
  background-color: #fff;
  color: #000;
  padding: 8px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
}

ul {
  border-radius: 10px;
  margin-top: 10px;
  background-color: #fff;
  color: #000;
  padding: 10px 0;
  display: none;
  z-index: 1;
  transition: 0.2s;
  position: absolute;
  border-bottom: 10px;
  width: 250px;
}

.menu_open {
  display: block;
}

ul li {
  border-bottom: 1px solid #000;
  padding: 12px;
  cursor: pointer;
  list-style: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

ul li:hover {
  background-color: #0000001e;
}

ul li:last-child {
  border-bottom: none;
}

.caret {
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 6px solid #0c0c0c;
  transition: 0.3s;
}

.caret_rotate {
  transform: rotate(180deg);
}

.div {
  height: 20px;
  width: 20px;
  background-color: #000;
  border: 1px solid grey;
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  display: none;
}

.display_button {
  display: flex;
}
.option_section{
  justify-content: start;
}
.chev{
  display: flex;
  align-items: center;
  gap: 10px;
}
option{
  color: red;
}
</style>
