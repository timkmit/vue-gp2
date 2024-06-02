<template>
    <div class="task-card">
        <TheTask class="task-card__created" :disabled="!isEdit" @keydown.enter="onSave" v-model:description="task.name" v-model:isChecked="task.checked" checkbox/>
      <div class="task-card__wrapper">
        <TheButton class="task-card__change" v-if="!isEdit" @click="onEdit" :icon="PenIcon">
        </TheButton>
        <TheButton class="task-card__save" v-else @click="onSave" :icon="SaveIcon" ></TheButton>
        <TheButton class="task-card__delete" @click="onDelete" :icon="BasketIcon"></TheButton>
      </div>
    </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';
import TheButton from "../buttons/TheButton.vue";
import PenIcon from "../icons/PenIcon.vue";
import SaveIcon from "../icons/SaveIcon.vue";
import BasketIcon from "../icons/BasketIcon.vue";
import TheTask from "./TheTask.vue";

const props = defineProps({
  task: {
    type: Object
  }
})
const value = ref(props.task.name)
const isEdit = ref(false)

const emit = defineEmits(["save", "delete","done"])

function onSave() {
    isEdit.value = false
}
function onEdit() {
  isEdit.value = true
}

function onDelete() {
  emit("delete", value.value)
}
</script>

<style scoped>
.task-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-left: 17px;
  background-color: #333333;
  border-radius: 8px;
}

.task-card__wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>

