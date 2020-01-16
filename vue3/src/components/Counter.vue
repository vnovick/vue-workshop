<template>
  <div>
      <div>
          {{ count }} 
     </div>
     <div>
         {{ counterPowerOf2 }}
     </div>
    <button @click="increment">
        +
    </button>
    <button @click="decrement">
        -
    </button>
  </div>
</template>

<script>
import { ref, computed, onMounted } from '@vue/composition-api'

function useCounter(initialCounterState, power){
    const count = ref(initialCounterState)
    const counterPowerOf2 = computed(() => Math.pow(count.value, power)) 
    function increment() {
        count.value++
    }
    function decrement() {
        count.value--
    }
    return {
        count, 
        counterPowerOf2,
        increment,
        decrement
    }
}

export default {
  setup() {
    const { count, increment, decrement, counterPowerOf2 } = useCounter(0, 2);
    onMounted(() => {
        count.value = 40;
        increment()
    })
    return {
      count,
      increment,
      counterPowerOf2,
      decrement
    };
  }
}
</script>