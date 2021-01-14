<template>
  <li
    class="dropdown-item"
    :class="{'is-disabled':disabled}"
  >
    <slot></slot>
  </li>
</template>

<script>
export default {
  name: 'DropdownItem',
  props: {
    disabled: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style>
.dropdown-item.is-disabled {
  pointer-events: none;
  background-color: transparant;
}
.dropdown-item.is-disabled a {
  color: #6c757d;
}
</style>
