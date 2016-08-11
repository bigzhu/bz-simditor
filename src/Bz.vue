<style lang=less>
</style>

<template>
  <textarea v-html="content" placeholder="在这里输入内容" autofocus></textarea>
</template>

<script>
  import Simditor from 'simditor'
  import 'simditor/styles//simditor.css'
  // import store from '../store'
  export default {
    props: {
      content: {
        type: String,
        required: true,
        twoWay: true
      }
    },
    components: {
    },
    data: function () {
      return {
      }
    },
    ready () {
      this.editor = new Simditor(
        {
          textarea: this.$el
          // optional options
        }
      )

      let _this = this
      this.editor.on('valuechanged',
        function (e, src) {
          console.log(src)
          _this.content = _this.editor.getValue()
        }
      )
    },
    methods: {
      addScript: function (url) {
        var script = document.createElement('script')
        script.type = 'text/javascript'
        script.src = url
        document.body.appendChild(script)
      }
    }
  }
</script>
