<script setup>
import SlotMachine from './components/SlotMachine.vue';
</script>

<template>
  <main>
    <h1>Counting with Slot Machines</h1>

    <div class="github-link">
      <img src="/github-logo.png" alt="github-logo" /> 
      <a href="https://github.com/gruhn/counting-with-slot-machines">Sources on Github</a>
    </div>

    <p>
      You probably heard the phrase before "computers only understand zeros and ones".
      Computers certainly can represent larger numbers,
      but for that they only use the digit symbols <b>0</b> and <b>1</b>.
      Computers use a <i>numeral system with a different base</i>.
      This system works pretty much the same as our familiar decimal system (with 0,1,2,3,4,5,6,7,9).
      To understand how it works you only have to un-learn one convention.
      <b>The set of symbols we use does not matter at all.</b>
      To really digest this, I find it most intuitive to visualize counting with slot machines.
      For example, the slot machine below shows counting in the decimal system.
      Imagine each digit as a spinning wheel with symbols printed on it.
      Click on the <b>+</b> button to increment the number by one.
    </p>

    <SlotMachine :init="1" :length="6" :symbols="[0,1,2,3,4,5,6,7,8,9]" />

    <p>
      We turn the right-most wheel to a higher-valued digit until we reach the highest-valued digit: <b>9</b>.
      After that the wheel goes back to <b>0</b> but with that we also its left-neighbor wheel once.
      If that digit is also already a <b>9</b>, it's also reset to <b>0</b> and the wheel to it's left is turned and so on.
    </p>

    <p>
      You know how it goes.
      What I want you to realize is that this way of counting also works if we use more symbols, fewer symbols or different symbols. 
      For example, we could remove the symbol <b>9</b>.
      What do we get if we count past <b>8</b>?
    </p>

    <SlotMachine :init="8" :length="6" :symbols="[0,1,2,3,4,5,6,7,8]" />

    <p>
      We immediately jump to "one-zero".
      The value of the number is not 10. 
      It's still 9, as we expect, but we don't have access to the symbol <b>9</b>, 
      so we represent the number as "one-zero".
      Keep incrementing the number up to "one-eight".
      What do you think comes next?
      What do you think are the digits if you increment past "eight-eight-eight"?
    </p>

    <SlotMachine :init="9**3 - 1" :length="6" :symbols="[0,1,2,3,4,5,6,7,8]" />

    <p>
      Instead of using fewer symbols, 
      we can also make up some arbitrary extra symbols.
      For example, let's declare that after <b>9</b> comes <b>A</b>;
      after that <b>🎵</b>; 
      and after that <b>💩</b>.
    </p>

    <SlotMachine :init="0" :length="6" :symbols="[0,1,2,3,4,5,6,7,8,9,'A','🎵','💩']" />

    <p>
      Now crucially, we can also use nothing but the symbols <b>0</b> and <b>1</b>.
      And this is the system computers use internally.
      Try it out and try to predict what the next number will be before you hit the 
      "+" button.
    </p>

    <SlotMachine :init="1" :length="6" :symbols="[0,1]" />
    
    <p>
      By the way, have you ever looked at the different iPhone available?
      At the time of writing there is a version with 64GB, 128GB and 256GB storage available.
      Why do they use these arbitrary numbers? 
      Why not just 60GB, 120GB and 250GB?
      And it's not just iPhones. 
      Laptops, USB sticks, ... any kind of hardware really.
      If you read the tech specs you'll see these numbers.
    </p>

    <p>
      The reason is, if you write these numbers in the numeral system of computers,
      they are actually the "clean" numbers:
    </p>

    <ul>
      <li>2 = 10</li>
      <li>4 = 100</li>
      <li>8 = 1000</li>
      <li>16 = 10000</li>
      <li>32 = 100000</li>
      <li>64 = 1000000</li>
      <li>128 = 1000000</li>
      <li>256 = 10000000</li>
      <li>...</li>
    </ul>

  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
