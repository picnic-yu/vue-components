<template>
  <div :class="classes">
    <nav>
      <button :class="['btn-pull',cssPrefix + 'header-back']" @click="backHandler" v-if="back!==false">
        <i class="iconfont">&#xe660;</i>
      </button>
      <div :class="[cssPrefix + 'header-title', back===false ? cssPrefix + 'header-title-center' : '']">
        <slot name="title"></slot>
      </div>
      <slot name="pull"></slot>
    </nav>
    <slot></slot>
  </div>
</template>

<script>
import { cssPrefix } from 'utils/variable.js'
export default {
  props: {
    back: {
      type: [String, Boolean, Function],
      default: true
    },
    backText: {
      type: String,
      default: '返回'
    }
  },
  computed: {
    classes () {
      return [cssPrefix + 'header']
    }
  },
  data () {
    return {
      cssPrefix: cssPrefix
    }
  },
  methods: {
    backHandler () {
      if (this.back === true) {
        history.back()
      }
      if (typeof this.back === 'string') {
        location.href = this.back
      }
      if (typeof this.back === 'function') {
        this.back()
      }
    }
  }
}
</script>

<style lang="scss">
  @import '~styles/variable.scss';
  @import '~styles/mixins.scss';
  .#{$css-prefix}{
    &header{
      background:#fff;
      nav{
        color:#fff;
        background-color:$primary-color;
        display:flex;
        align-items:center;
        height:2.7rem;
      }
      .btn-pull{
        color:inherit;
        height:inherit;
        min-width: 40px;
        text-align: center;
        @include button;
        @include active;
      }
      &-back{
        margin-right:-10px;
        position:relative;
        z-index:1;
        &:active{
          background:transparent!important;
        }
      }
      &-title{
        flex:1;
        font-size:1.1rem;
        overflow: hidden;
        &-center{
          text-align:center;
        }
      }
    }
  }
</style>
