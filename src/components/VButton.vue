<script setup lang="ts">
type Size = 'xl' | 'm' | 'l' | 's' | 'round'

type Color =
  | 'wight'
  | 'wight-light'
  | 'blue'
  | 'blue-light'
  | 'red'
  | 'gray'
  | 'red-light'
  | 'b-to-g'

interface Props {
  size?: Size
  color?: Color
  disabled?: boolean
  bgEmpty?: boolean
}

withDefaults(defineProps<Props>(), {
  size: 'xl',
  color: 'blue',
  disabled: false,
  bgEmpty: false
})
</script>

<template>
  <button
    class="button"
    :class="[`button-${size}`, `button-${color}`, { 'button-bgEmpty': bgEmpty }]"
    v-bind="disabled ? { 'aria-disabled': 'true', disabled: true } : {}"
  >
    <slot />
  </button>
</template>

<style scoped>
.button {
  position: relative;
  font-family: 'Inter Display', sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 19.36px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: all 0.2s ease-in-out;
}

.button-round {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 8px;
  border-radius: 1000px;
}

[aria-disabled='true'] {
  pointer-events: none;
}

.button-xl {
  width: 100%;
  height: 52px;
  font-size: 16px;
  line-height: 19.36px;
  border-radius: 12px;
}

.button-l {
  height: 40px;
  padding: 0 67px;
  border-radius: 12px;
}

.button-m {
  height: 40px;
  padding: 0 37px;
  border-radius: 8px;
}

.button-s {
  height: 32px;
  padding: 0 61px;
  border-radius: 8px;
}

.button-blue {
  color: #fff;
  background-color: #027dff;
}

.button-blue:hover {
  background-color: #0072ea;
}

.button-blue:active {
  background-color: #016ee1;
}

.button-blue-light {
  color: var(--color-blue);
  background-color: #e0efff;
}

.button-b-to-g {
  color: var(--blue-to-wight);
  background-color: var(--btn-bg);
}

.button-blue-light:hover {
  background-color: #d3e7fc;
}

.button-blue-light:active {
  background-color: #027dff;
}

.button-red {
  color: #fff;
  background-color: #fe015c;
}

.button-red:hover {
  background-color: #e90054;
}

.button-red:active {
  background-color: #dc004f;
}

.button-wight {
  color: #027dff;
  background-color: #fff;
}

.button-wight:hover {
  background-color: #fffc;
}

.button-wight:active {
  background-color: #fff6;
}

.button-wight[aria-disabled='true'] {
  color: #9d9d9d;
  cursor: default;
  background-color: #e6e6e6;
}

.button-wight-light {
  color: #fff;
  background-color: #ffffff26;
}

.button-wight-light:hover {
  color: #027dff;
  background-color: #ffffff40;
}

.button-wight-light:active {
  background-color: #fff6;
}

.button-gray {
  color: var(--color-black);
  background-color: var(--g1-to-gb);
}

.button-gray:hover {
  background-color: var(--g2-to-g4);
}

.button-gray:active {
  background-color: #dcdcdc;
}

.button-gray[aria-disabled='true'] {
  color: #9d9d9d;
  cursor: default;
  background-color: #e6e6e6;
}

.button-bgEmpty {
  padding: 0;
  background-color: transparent;
}

.button-bgEmpty:hover {
  background-color: transparent;
}

.button-red-light {
  color: var(--color-red);
  background: var(--color-wight);
}
</style>
