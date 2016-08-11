<style lang=less>
</style>

<template>
  <div>
    <doc name="bz-simditor"
      desc="富文本编辑"
      parm_desc="编辑"
      :parms="parms"
      :code="code"
      >
      <div v-html="content"></div>
      <bz :content.sync="content"></bz>
    </doc>
  </div>
</template>

<script>
  import 'bz-semantic-ui-card'
  import 'bz-semantic-ui-grid'
  import Bz from './Bz'
  import Doc from 'bz-doc'
  export default {
    components: {
      Bz,
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
        datas: [1],
        parms: [
          {parm: 'el', desc: '使用该组件的el,主要为了把查找last限定在本el中. !注意, fragment的el是无法传递进去的'},
          {parm: 'element_class', desc: '用于定位last的class .hah.jj 的格式'},
          {parm: 'call_back', desc: '滚到底部的回调函数'}
        ],
        parm_desc: `注意，如果使用的组件有路由，那么最好在切换路由的时候发送消息，解除绑定(参看本例子) <code>this.$broadcast('unbind-scroll')</code>`,
        code: `<bottom-loader :el="$el" element_class=".ui.card" :call_back="call_back"></bottom-loader>`
      }
    },
    methods: {
      call_back: function () {
        this.datas.push(this.datas.length + 1)
      }
    }
  }
</script>
