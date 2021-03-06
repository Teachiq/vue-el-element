<template>
<input
  :value="value"
  @change="contentChanged"
  @keyup="duringChange"
  @input="$emit('input', $event.target.value)"
  class='el-input el-animation'
  :class="{
    'el-input--warning' : warning,
    'el-input--success' : success,
    [marginClassName]: true,
  }"
  :type='type'
  :placeholder="placeholder"
  ref="inputField"
  >
</template>
<script>
import margin from '@/util/mixins/margin'

export default {
  name: 'ElInput',
  mixins: [margin],
  props: {
    placeholder: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: ''
    },
    warning: {
      type: Boolean,
      default: false
    },
    success: {
      type: Boolean,
      default: false
    },
    focus: {
      type: Boolean,
      default: false
    }
  },
  watch: {
    focus (isFocus) {
      if (isFocus && this.$el) {
        this.$el.focus()
      }
    }
  },
  mounted () {
    if (this.focus && this.$el) {
      this.$el.focus()
    }
  },
  methods: {
    contentChanged (ev) {
      this.$emit('change', this.value)
    },
    duringChange (ev) {
      if (ev.keyCode === 13) {
        this.$refs.inputField.blur()

        this.$emit('enter', this.value)

        ev.preventDefault()
        return false
      }

      this.$emit('keyup', this.value)
    }
  }
}

</script>

<style scoped lang="less">
  @import '~el-style/variables.less';

  .el-input {
    position: relative;
    flex-grow: 1;
    width: 100%;
    height: @input-height;
    min-height: @input-height;
    text-align: left;
    background-color: @input-background;
    padding-left: @input-padding;

    border-radius: @input-radius;
    border: @input-border;
    outline: none;
    box-sizing: border-box;

    &:focus {
      border: @input-border-focus;
    }

    &--warning {
      color: @color-danger-7;
      border-color: @color-danger-7;
      background-color: @color-danger-1;
    }

    &--success {
      color: @color-success-7;
      border-color: @color-success-7;
      background-color: @color-success-1;
    }
  }
</style>
