<style lang=less>
</style>

<template>
  <div>
    <doc name="bz-simditor"
      desc="富文本编辑"
      :parm_desc="parm_desc"
      :parms="parms"
      :code="code"
      :call_back="call_back"
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
    },
    data: function () {
      return {
        content: '',
        parms: [
          {parm: 'content', desc: 'html的内容'}
        ],
        parm_desc: ``,
        code: `<bz :content.sync="content"></bz>`
      }
    },
    methods: {
      call_back: function () {
        this.content = '<b>bigzhu</b>'
      }
    }
  }
</script>
