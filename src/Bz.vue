<style lang=less>
</style>

<template>
  <textarea v-html="content" placeholder="在这里输入内容" autofocus></textarea>
</template>

<script>
  import Simditor from 'simditor'
  // import 'simditor/styles//simditor.css'
  export default {
    props: {
      content: {
        type: String,
        required: true,
        twoWay: true
      }
    },
    watch: {
      'content': function (val, oldVal) {
        if (val !== oldVal) {
          this.editor.setValue(val)
        }
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
            fileKey: 'file',
            connectionCount: 3,
            leaveConfirm: '图片正在上传, 确定要离开该页面?'
          },
          pasteImage: true
        }
      )

      let _this = this
      this.editor.on('valuechanged',
        function (e, src) {
          if (_this.content !== _this.editor.getValue()) _this.content = _this.editor.getValue()
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
