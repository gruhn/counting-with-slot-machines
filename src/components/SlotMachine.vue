<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  symbols: Array,
  length: Number,
  init: Number,
})

const value = ref(props.init)

const digitsOf = function* (base, num) {
  const first = num % base
  yield first
  yield* digitsOf(base, (num - first) / base)
}

const take = function* (n, gen) {
  if (n > 0) {
    yield gen.next().value
    yield* take(n - 1, gen)
  }
}

const inc = () => {
  value.value = (value.value + 1) % (props.symbols.length**props.length)
}

const digits = computed(() => {
  const base = props.symbols.length
  const xs = take(props.length, digitsOf(base, value.value))
  return [...xs].reverse().map(x => props.symbols[x])
})
</script>

<template>
  <div class="slot-machine">
    <ul class="wheels">
      <li v-for="digit in digits" class="wheel">
        <transition name="roll">
          <div class="digit" :key="digit">{{ digit }}</div>
        </transition>
      </li>
    </ul>

    <button @click="inc">+</button>
  </div>
  value   = {{ value }};
  symbols = {{ symbols.map(String).join(", ") }}
</template>

<style scoped>
.slot-machine {
  display: flex;
  flex-direction: row; 
  align-items: stretch;

  font-family: monospace;
  font-weight: bold;
  font-size: 2rem;
  text-align: center;
  color: #7e0505;
}

.slot-machine button {
  background-color: #ffecc7;
  border: 2px solid #613511;

  cursor: pointer;
  font-size: inherit;
  color: inherit;

  box-sizing: content-box;
  width: 1cm;

  margin-left: 10px;
}

.wheels {
  display: flex;
  margin-bottom: 5px;
  margin: 0;
  padding: 0;
}
.wheel {
  list-style-type: none;
  position: relative;
  height: 1em;
  width: 1.5ch;
  padding: 10px; 

  border: 2px solid #613511;
  margin-left: -2px;

  background-color: #ffecc7;
  overflow: hidden;
  box-sizing: content-box;
}
.wheel .digit {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
  width: inherit;
}
.wheel::before,
.wheel::after {
  content: ' ';
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  height: 33%;
  z-index: 2;
}
.wheel::before {
  top: 0;
  background-image: linear-gradient(#00000085, transparent);
}
.wheel::after {
  bottom: 0;
  background-image: linear-gradient(transparent, #00000085);
}

.roll-enter-active,
.roll-leave-active {
  transition: all .1s linear;
}
.roll-enter-from {
  transform: translateY(-150%) !important;
}
.roll-enter-to,
.roll-leave-from {
  transform: translateY(-50%) !important;
}
.roll-leave-to {
  transform: translateY(50%) !important;
}
</style>