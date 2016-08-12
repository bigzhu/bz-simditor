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
          textarea: this.$el,
          upload: {
            url: '/api_file_upload',
            params: null,
            fileKey: 'upload_file',
            connectionCount: 3,
            leaveConfirm: 'Uploading is in progress, are you sure to leave this page?'
          }
        }
      )
      let _this = this
      this.editor.on('valuechanged',
        function (e, src) {
          console.log(src)
          console.log(e)
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
