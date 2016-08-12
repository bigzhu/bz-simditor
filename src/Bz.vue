<style lang=less>
</style>

<template>
  <textarea v-html="content" placeholder="在这里输入内容" autofocus></textarea>
</template>

<script>
  import $ from 'jquery'
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
            leaveConfirm: '图片正在上传, 确定要离开该页面?'
          }
        }
      )
      let _this = this
      this.editor.on('valuechanged',
        function (e, src) {
          _this.content = _this.editor.getValue()
          var $img = $(_this.content).find('img')
          if ($img && /^data:image/.test($img.attr('src'))) {
            console.log($img.attr('alt'))
          }
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
