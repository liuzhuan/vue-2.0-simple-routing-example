<template>
  <a
    v-bind:href="href"
    v-bind:class="{ active: isActive }"
    v-on:click="go"
  >
    <slot></slot>
  </a>
</template>

<script>
  import routes from '../routes'

  export default {
    props: {
      href: {
        type:String,
        required: true 
      }
    },
    computed: {
      isActive () {
        /**
         * `vm.$root`: 当前组件树的根 Vue 实例。如果当前实例没有父实例，此实例将会是其自己。
         * 
         * https://cn.vuejs.org/v2/api/#vm-root
         */
        return this.href === this.$root.currentRoute
      }
    },
    methods: {
      go (event) {
        event.preventDefault()
        this.$root.currentRoute = this.href
        window.history.pushState(
          null,
          routes[this.href],
          this.href
        )
      }
    }
  }
</script>

<style scoped>
  .active {
    color: cornflowerblue;
  }
</style>
