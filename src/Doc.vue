<template>
  <div>
    <doc name="bz-simditor"
      desc="富文本编辑"
      :parm_desc="parm_desc"
      :parms="parms"
      :code="code"
      :call_back="call_back"
      >
      <div v-html="content.text"></div>
      <bz :content="content"></bz>
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
    mounted () {
      let self = this
      this.$nextTick(function () {
        setTimeout(() => { self.content.text = 'change the file' }, 2000)
      })
    },
    data: function () {
      return {
        content: {
          text: ''
        },
        parms: [
          {parm: 'content.text', desc: 'html的内容'}
        ],
        parm_desc: ``,
        code: `<bz :content="content"></bz>`
      }
    },
    methods: {
    }
  }
</script>
