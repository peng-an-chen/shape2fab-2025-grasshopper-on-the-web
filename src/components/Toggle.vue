<script setup>
import { ref } from "vue"

// Define props
const props = defineProps(['title', 'val'])

const title = ref(props.title)
// Define emits
const emits = defineEmits(['update'])

// Define variables with refs
var toggleValue = ref(props.val)

function emitValueUpdate()
{
  emits("update", toggleValue.value, title.value)
}
</script>


<template>
  <div id="toggle-container">
  <div>
  <form class="definition-input">
    <label class="switch">
      <input type="checkbox"
             :id="title"
             v-model="toggleValue"
             @change="emitValueUpdate" />
      <span class="slider"></span>
    </label>
  </form>

  </div>
  <div id="title">
    <span class="input-title">{{ title }} </span>
  </div>
 </div>
</template>

<style scoped>
#toggle-container {
  font-size: 1rem;
  padding: 3px;
  display: flex;
}

#title{

  margin-left: 10px;
}

.definition-input {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 8px;
}

/* Clean switch styling */
.switch {
  position: relative;
  display: inline-block;
  width: 50px;
  height: 25px;
}

/* Hide default checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* Slider background */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0; left: 0; right: 0; bottom: 0;
  background-color: var(  --vt-c-slate-200);
  transition: 0.4s;
  border-radius: 25px;
}

/* Knob */
.slider::before {
  content: "";
  position: absolute;
  height: 21px;
  width: 21px;
  left: 2px;
  bottom: 2px;
  background-color: var(--custom-color);
  transition: 0.4s;
  border-radius: 50%;
}

/* Move knob when checked */
.switch input:checked + .slider::before {
  transform: translateX(25px); /* Fixed: added px */
  
}

/* ON state (when checkbox is checked) */
.switch input:checked + .slider {
  background-color: var(--global-light); /* Keep or adjust */
}

.switch input:checked + .slider::before {
  background-color: var(--custom-color); /* Already looks good */
}

/* OFF knob color (optional if you want dimmer knob too) */
.switch input:not(:checked) + .slider::before {
  background-color: #888; /* Dim the knob when off */
}


</style>
