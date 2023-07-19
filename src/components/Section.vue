<script setup>
import dataBD from '@/mocks/data.js'

import Button from "@/components/Button.vue";
import Input from "@/components/Input.vue";

import { computed, ref } from 'vue';

const data = ref(Object.assign(dataBD));

const editingIndex = ref(null);
const inputVal = ref("");

const editingName = computed(() => {
  return data.value[editingIndex.value].name;
})

const editItem = (index) => {
  editingIndex.value = index;
  inputVal.value = data.value[index].value;
};

const saveItem = () => {
  data.value[editingIndex.value].value = inputVal.value;
  // cancelEdit();
};

const cancelEdit = () => {
  editingIndex.value = null;
  inputVal.value = "";
};

const activeItem = (index) => {
  if (!editingIndex.value) return
  return [{'--active': editingIndex.value === index}]
}

</script>

<template>
  <section class="section">
    <div class="section__container container" v-auto-animate>
      <h2 class="section__title">
        Выберете объект значение которого хотите поменять
      </h2>
      <div class="select">
        <button
          v-for="(item, index) in data"
          :key="index"
          class="select__option"
          :class="activeItem(index)"
          @click="editItem(index)"
        >
          {{ item.name }}
        </button>
      </div>
      <div
        v-if="editingIndex !== null"
        class="edited"
      >
        <div class="edited__body">
          <div class="edited__label">
            Введете новое значение для
            <span class="edited__label--name">
              {{ editingName }}:
            </span>
          </div>
          <Input
            v-model="inputVal"
            class="edited__input"
            @keyup.enter="saveItem"
            @blur="cancelEdit"
          />
          <span class="edited__info">
            для сохранения нажмите 'Enter' или кнопку 'Save'
          </span>
        </div>
        <Button
          class="edited__button"
          @click="saveItem"
        >
          Save
        </Button>
        <div class="edited__footer">
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>

.section {
  display: flex;
  width: 100%;
  
  // .section__title
  &__title {
    margin-bottom: 32px;
    text-align: center;
    font-size: 28px;
    font-weight: 600;
  }
  
  // .section__container
  &__container {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 560px;
  }
}


.select {
  display: grid;
  grid-gap: 8px;
  grid-template-columns: repeat( auto-fit, minmax(80px, 1fr));
  width: 100%;
  margin-bottom: 32px;
  
  // .select__option
  &__option {
    padding: 4px 12px;
    background: var(--c-active);
    border-radius: 4px;
    color: initial;
    font-size: inherit;
    transition: opacity .2s ease-in-out;
    
    &:hover {
      opacity: .8;
      
    }
    
    &.--active {
      opacity: .6;
      
    }
  }
}

// .edited
.edited {
  display: grid;
  grid-gap: 16px;
  
  // .edited__body
  &__body {
    display: grid;
    grid-gap: 4px;
  }
  
  // .edited
  &__label {
    &--name {
    font-weight: 600;
      border-bottom: 1px solid var(--c-active);
    }
  }
  
  // .edited__input
  &__input {
    text-align: end;
  }
  
  // .edited__info
  &__info {
    font-size: 12px;
  }
  
  // .edited
  &__button {
  
  }
}
</style>
