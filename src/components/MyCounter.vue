<script setup>
import { ref, computed, onBeforeMount, onMounted,
  onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted,
  customRef, defineProps, defineEmits, inject} from 'vue';

console.log("setup: The component is created in memory");

let timer = ref(null);
const maxCount = 10;

// 声明init和end两个 attributes
const props = defineProps(["limits", "index"]);
const init = props.limits.init || 0;
const end = props.limits.end || 0;
const index = props.index || 1;

// const count = ref(0);
const count = ref(parseInt(init));

const emit = defineEmits(["incr"]);

const total = inject('app.total');

function decrement() {
    count.value--;

}
const clickMe = () => {
  alert('You clicked me!');
}

const doubleCount = computed(() => count.value * 2);

const increment = () => {
  if (!end || count.value < parseInt(end)) {
    count.value++;
    // 发送事件
    emit("incr", 1);
    total.value++;
  } else {
    stop();
  }
};

const start = () => {
  timer.value = setInterval(() => {
  increment();  
  }, 1000);
};

const stop= () => {
  clearInterval(timer.value);
  timer.value = null;
};

// Lifecycle hooks
onBeforeMount(() => {
  console.log("onBeforeMount: The component is about to be mounted");
});
onMounted(() => {
  console.log("onMounted: The component has been mounted");
  start();
});
onBeforeUpdate(() => {
  console.log("onBeforeUpdate: The component is about to be updated");
});
onUpdated(() => {
  console.log("onUpdated: The component has been updated");
});
onBeforeUnmount(() => {
  console.log("onBeforeUnmount: The component is about to be unmounted");
});
onUnmounted(() => {
  console.log("onUnmounted: The component has been unmounted");
  stop();
});

const count2 = customRef((track, trigger) => {
  let value = 0;
  return {
    get() {
      // Track the dependency when the value is accessed

      track();
      console.log("get call track: The value is ", value);
      return value;
    },
    set(newValue) {
      // customized logic to set the value depending on the condition
      // Update the value and trigger reactivity when the value is changed
      if (newValue <= maxCount) {
        // only update the value if it is less than or equal to maxCount
        value = newValue;
      }
      
      trigger();
      console.log("set call trigger: The value is ", value);
    }
  };
});

const useMaximum = (max) => {
  // Create a custom reference (customRef)
  return customRef((track, trigger) => {
  let value = 0;
  return {
    get() {
      // Track the dependency when the value is read.
      track();
      return value;
    },
    set(newValue) {
      // Update the value and trigger reactivity.
      if (newValue <= max) value = newValue;
        trigger();
      }
    };
  });
}

const count3 = useMaximum(5);
const incrementCount3 = () => {
  count3.value++;
}

const verifyKey = () => {
  const numbers = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"];
  const moves = ["Backspace", "ArrowLeft", "ArrowRight", "Delete", "Tab", "Home", "End"];
  let authorized;
  authorized = [...numbers, ...moves];
  if (!authorized.includes(event.key)) {
    event.preventDefault();
  }
}
</script>
<!-- <script>
export default {
  name: 'MyCounter'
}
</script> -->

<template>
  <h1>MyCounter Component - {{ index }}</h1>
  <p class="fc"> First Component </p>
  Reactive variable count: {{ count }} 
  <br>
  init: {{ init }} => end: {{ end }}
  <br>
  <button @click="count++">Increment</button>
  <button @click="decrement()">Decrement</button>
  <button @click="clickMe()">Click Me</button>
  <br>
  Computed variable doubleCount: {{ doubleCount }}
  <hr>
  Custom Ref count2: {{ count2 }}
  <button @click="count2++">Increment</button>
  <hr>
  Custom Ref count3: {{ count3 }}
  <button @click="incrementCount3">Increment</button>
  <hr>
  Input: <input type="text" v-bind:value="count" />
  Input for count (using v-model): <input type="text" v-model="count" />
  <hr>
  <!-- <button v-if="!timer" @click="start()">Start</button>
  <button v-else @click="stop()">Stop</button> -->
  <button v-show="!timer" @click="start()">Start</button>
  <button v-show="timer" @click="stop()">Stop</button>
  <hr>
  Reactive variable count: <input type="text" v-model="count" @keydown="verifyKey" />
  <br>
  Enterd value: {{ count }}
</template>

<style scoped>
h1 {
  color: red;
  font-family: 'Courier New', Courier, monospace;
  font-size: 20px;
}
.fc {
  color: blue;
}
</style>