<template>
  <div ref="renderBox" class="box" />
</template>

<script>
import element from 'element-ui/lib/theme-chalk/index.css'
import 'amis/lib/themes/default.css'
// import "amis/lib/themes/antd.css";
// import "amis/lib/themes/cxd.css";
import { alert, confirm, render as renderSchema, toast } from 'amis'
// import copy from 'copy-to-clipboard'
import ReactDOM from 'react-dom'
// import * as qs from 'qs'
// import axios from 'axios'

export default {
  name: 'Amis',
  props: {
    schema: {
      type: Object,
      required: false,
      default: function() {
        return {}
      }
    },
    onAction: {
      type: Function,
      required: false,
      default: () => {}
    }
  },
  data() {
    return {
      theme: 'default'
      // theme: element

    }
  },
  watch: {
    schema: function(newSchema, oldSchema) {
      this.initPage(newSchema)
    }
  },
  mounted() {
    this.initPage(this.schema)
  },

  methods: {
    initPage(schema) {
      // this.initEnv()
      ReactDOM.render(
        renderSchema(
          schema,
          {
            onAction: this.onAction || this.handleAction,
            theme: this.theme
          },
          this.env
        ),
        this.$refs.renderBox
      )
    },
    handleAction(e, action) {
      this.env.alert(`没有识别的动作：${JSON.stringify(action)}`)
    }
  }
}
</script>
<style lang="scss" scoped>
</style>
