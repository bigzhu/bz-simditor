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
      <bz v-model="content"></bz>
    </doc>
  </div>
</template>

<script>
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
        setTimeout(() => { self.content = 'change the file' }, 2000)
      })
    },
    data: function () {
      return {
        content: '',
        parms: [
          {parm: 'v-model', desc: 'html的内容'}
        ],
        parm_desc: ``,
        code: `<bz v-model="content"></bz>`
      }
    },
    methods: {
    }
  }
</script>
