<template>
  <textarea placeholder="在这里输入内容"></textarea>
</template>

<script>
  import Simditor from 'simditor'
  export default {
    props: {
      content: {
        type: String,
        required: true,
        twoWay: true,
        default: ''
      }
    },
    /* 由于上传文件的特殊处理，导致无法用下面的代码实现真正的动态绑定, 只有第一次传值进去 */
    watch: {
      'content': function (val, oldVal) {
        if (this.editor.getValue() === '' || val === '') this.editor.setValue(val)
      }
    },
    components: {
    },
    data: function () {
      return {
      }
    },
    mounted () {
      this.$nextTick(function () {
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
            pasteImage: false
          }
        )

        let _this = this
        this.editor.on('valuechanged',
          function (e, src) {
            if (_this.content !== _this.editor.getValue()) _this.content = _this.editor.getValue()
          }
        )
        this.editor.setValue(this.content)
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
