<template>
  <div class="test-block">
    <valid-reg :reg.sync="regg" showInfo showStep readOnly></valid-reg>
    <regulex :reg="regg"></regulex>
  </div>
</template>
<style scoped>
</style>
<script>
  import regulex from './regulex.vue'
  import validReg from './validReg.vue'
  export default {
    data() {
      return {
        regg: ''
      }
    },
    components: {regulex, validReg},
    created () {
      this.regg = this.reg
    },
    props: {
      reg: [String],
      showInfo: [Boolean],
      showStep: [Boolean],
      readOnly: [Boolean],
    }
  }
</script>
