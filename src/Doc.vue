<style lang=less>
</style>

<template>
  <div>
    <doc name="bz-simditor"
      desc="富文本编辑"
      :parms="parms"
      :code="code"
      >
      <div v-html="content"></div>
      <div v-for="file in files">
        图片路径: {{file}}
      </div>
      <simditor :content.sync="content" :files.sync="files"></simditor>
    </doc>
  </div>
</template>

<script>
  import 'bz-semantic-ui-card'
  import 'bz-semantic-ui-grid'
  import simditor from './Bz'
  import Doc from 'bz-doc'
  export default {
    components: {
      simditor,
      Doc
    },
    route: {
      deactivate: function (transition) {
        this.$broadcast('unbind-scroll')
        console.log('解除了scroll绑定')
        transition.next()
      }
    },
    data: function () {
      return {
        content: '<b>bigzhu</b>',
        files: [],
        datas: [1],
        parms: [
          {parm: 'content', desc: '编辑器内容'},
          {parm: 'files', desc: '上传的图片路径list'}
        ],
        parm_desc: `注意，如果使用的组件有路由，那么最好在切换路由的时候发送消息，解除绑定(参看本例子) <code>this.$broadcast('unbind-scroll')</code>`,
        code: `<simditor :content.sync="content" :files.sync="files"></simditor>`
      }
    },
    methods: {
    }
  }
</script>
