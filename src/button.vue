<template>
  <button class="g-button" :class=`icon-${iconPosition}` @click="$emit('click')">
    <g-icon class="icon" v-if="icon && !loading" :name="icon"></g-icon>
    <g-icon v-if="loading" class="loading icon" name="loading"></g-icon>
    <span class="content">
      <slot></slot>
    </span>
  </button>
</template>

<script>
export default {
  props: {
    icon: {},
    iconPosition: {
      type: String,
      default: 'left',
      validator(value) {
        return value !== 'left' || value !== 'right';
      }
    },
    loading: {
      type: Boolean,
      default: false
    }
  },
  created() {
    console.log(1);
  }
}
</script>

<style scoped lang="scss">
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.g-button {
  font-size: var(--font-size);
  height: var(--button-height);
  padding: 0 1em;
  border-radius: var(--border-radius);
  border: 1px solid var(--border-color);
  background: var(--button-bg);
  display: inline-flex;
  vertical-align: middle;
  justify-content: center;
  align-items: center;

  &:hover {
    cursor: pointer;
    border-color: var(--border-color-hover)
  }

  &:active {
    background-color: var(--button-active-bg)
  }

  &:focus {
    outline: none;
  }

  .icon {
    order: 1;
    margin-right: .3em;
  }

  .content {
    order: 2;
  }

  &.icon-right {
    .icon {
      order: 2;
      margin-left: .3em;
      margin-right: 0;
    }

    .content {
      order: 1;
    }
  }
  .loading {
    animation: spin 2s infinite linear;
  }
}

</style>