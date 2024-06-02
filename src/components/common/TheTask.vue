<template>
  <div class="task">
      <div class="task__checkbox-container" :class="{'dynamic': isChecked}" v-show="checkbox">
          <input type="checkbox" class="task__checkbox-input" v-model="checkboxValue" >
      </div>
    <textarea class="task-primary-textarea" v-model="textareaValue" :placeholder="placeholder" :disabled="disabled"></textarea>
  </div>
</template>

<script setup>
import {computed} from "vue";

const props = defineProps({
 description: {
    type: String,
    default:""
  },
  isChecked: {
    type: Boolean,
    default:false
  },
  placeholder: {
    type: String,
    default:""
  },
  checkbox: {
    type: Boolean,
    default:false
  },
  disabled: {
    type: Boolean,
    default:false
  }
})

const emit = defineEmits(["update:isChecked","update:description"])

const checkboxValue = computed({
  get() {
    return props.isChecked
  },
  set(value) {
    emit("update:isChecked",value)
  }
})

const textareaValue = computed({
  get() {
    return props.description
  },
  set(value) {
    emit("update:description",value)
  }
})
</script>

<style scoped>
.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width:100%;
}

.task-primary-textarea {
  border: 1px solid transparent;
  font-size: 18px;
  line-height: 18px;
  font-weight: 400;
  border-radius: 8px;
  padding: 6px 17px;
  background-color: #333333;
  color: #F2F2F2;
  width: 100%;
  box-sizing: border-box;
  resize: none;
  align-content: center;
  outline: 0;
  outline-offset: 0;
}

.task__checkbox-container {
  display: inline-block;
  cursor: pointer;
  position: relative;
  top: 1px;
  left: 0;
  height: 18px;
  width: 18px;
  background-color: transparent;
  border: 2px solid #4EA8DE;
  transition: background-color 0.25s ease-out;
  border-radius: 50%;
}

.dynamic {
  background-color: #5E60CE;
  border-color: #5E60CE;
  transition: background-color 0.25s ease-out, border-color 0.25s ease-out;
}

.dynamic::before {
  content: '✓';
  position: absolute;
  top: -1px;
  left: 1px;
  opacity: 1;
  transition: opacity 0.25s ease-out;
  color: white;
}

.task__checkbox-input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  top: 0;
  left: 0;
}

</style>

