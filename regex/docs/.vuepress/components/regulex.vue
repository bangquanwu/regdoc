<template>
  <div class="regulex">
  </div>
</template>
<style scoped>
.regulex{
  overflow-x: auto;
  /* text-align:center; */
}
</style>
<script>
  let raphael = req('regulex').Raphael;
  let parse = req('regulex').parse;
  let visualize = req('regulex').visualize;
  let Kit = req('regulex').Kit;
  export default {
    data() {
      return {
        msg: 'Hello this is <demo-component>'
      }
    },
    props: {
      reg: [String],
    },
    methods: {
      visual(){
        let ret = parse(this.reg)
        visualize(ret, [], this.paper)
      }
    },
    watch: {
      reg(){
        this.visual()
      }
    },
    mounted(){
      this.paper = raphael(this.$el, 10, 10)
      this.visual()
    }
  }
</script>
