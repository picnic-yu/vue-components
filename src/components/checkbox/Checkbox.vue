<template>
  <label :class="classes" :disabled="disabled" >
    <input type="checkbox" :name="name" :value="value" :disabled="disabled" :checked="checked" @change="changeHandler"/>
    <i :class="[cssPrefix + 'checkbox-icon','iconfont']">&#xe632;</i>
    <slot></slot>
  </label>
</template>

<script>
import { cssPrefix } from 'utils/variable.js'
import { input } from 'utils/mixins.js'
export default {
  mixins: [input],
  computed: {
    classes () {
      return [cssPrefix + 'checkbox', this.direction === 'reverse' ? cssPrefix + 'checkbox-reverse' : '']
    }
  },
  props: {
    direction: {
      type: String,
      default: 'normal'
    }
  },
  data () {
    return {
      cssPrefix: cssPrefix
    }
  },
  methods: {
    changeHandler (e) {
      this.$emit('on-change', e)
    }
  }
}
</script>

<style lang="scss">
  @import '~styles/variable.scss';
  @import '~styles/mixins.scss';
  .#{$css-prefix}{
    &checkbox{
      display:block;
      position:relative;
      padding:0.86rem 0.5rem;
      @include disabled;
      input{
        position:absolute;
        top:0;
        left:0;
        width:100%;
        height:100%;
        z-index:1;
        opacity:0;
        padding:0;
        margin:0;
      }
      &-icon{
        width:20px;
        height:20px;
        box-shadow:0 0 1px #666 inset;
        border-radius:20px;
        display:inline-block;
        transition:all 0.2s $ease-in-out;
        margin-right:4px;
        text-align: center;
        vertical-align: middle;
        color:transparent;
        line-height: 1.3;
        font-size: 16px;
      }
      &-reverse{
        .#{$css-prefix}checkbox-icon{
          position:absolute;
          top:50%;
          right:0.5rem;
          margin-top:-10px;
        }
      }
      input:checked + &-icon{
        background-color:$primary-color;
        box-shadow:none;
        color:#fff;
      }
    }
    
  }
</style>
