<script setup>
import { computed, defineProps } from "vue";

const props = defineProps({
  colorBtn: {
    type: String,
    validator(value) {
      return ['primary', 'secondary', 'tertiary'].indexOf(value) !== -1;
    },
    default: 'primary'
  },
  isDisabled: {
    type: Boolean,
    default: false
  },
  isRound: {
    type: Boolean,
    default: false
  },
  loading: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['click'])
const clickButton = () => {
  emit('click')
}

const mainClass = computed(() => {
  const button = 'button'
  const modification = {
    [`${button}--${props.colorBtn}`]: props.colorBtn,
    [`${button}--disabled`]: props.isDisabled,
    [`${button}--round`]: props.isRound,
    [`${button}--loading`]: props.loading
  }
  
  return [button, modification]
})
</script>

<template>
  <button
    :class="mainClass"
    :disabled="props.isDisabled"
    @click="clickButton"
  >
    <slot/>
  </button>
</template>

<style scoped lang="scss">
.button {
  --radius: 8px;
  
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 42px;
  min-height: 42px;
  padding: 12px 16px;
  background: inherit;
  border: none;
  border-radius: var(--radius);
  cursor: pointer;
  color: var(--color-text-button);
  font-size: inherit;
  font-weight: 600;
  transition: background var(--transition),
  color var(--transition);
  
  &--primary {
    --border: var(--vt-c-main);
    --border-hover: var(--vt-c-main-1);
    
    box-shadow: inset 0 0 0 2px var(--border);
    transition: box-shadow var(--transition);
    
    &:enabled:active,
    &:enabled {
      @media (hover: hover) {
        &:hover {
          box-shadow: inset 0 0 0 2px var(--border-hover);
        }
      }
    }
  }
  
  &--secondary {
    background: var(--vt-c-main);
    color: var(--color-text-button-color);
    
    &:enabled:active,
    &:enabled {
      @media (hover: hover) {
        &:hover {
          
          
          background: var(--vt-c-main-1);
        }
      }
    }
  }
  
  &--round {
    --radius: 32px;
  }
  
  &:disabled,
  &--disabled {
    cursor: default;
    opacity: .6;
    pointer-events: none;
  }
  
  &--loading {
    color: #0000;
  }
}
</style>
