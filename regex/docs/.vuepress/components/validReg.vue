<template>
  <div class="valid-reg" :class="valid?'pass':valid===false?'error':''">
    <input type="text" class="reg" v-model="rege" :readOnly="readonly" placeholder="正则" @dblclick="readonly=false">
    <br/>
    <input type="text" class="flags" v-model="flags"  placeholder="匹配模式">
    <br/>
    <input type="text" class="input" v-model="value" placeholder="待匹配字符串">
    <div v-if="showInfo" class="show-info">{{info}}</div>
  </div>
</template>
<style scoped>
input{
  line-height: 1.2;
  border-radius: 5px;
  font-size: 16px;
  width: 100%;
  min-width: 180px;
}
input[readonly]{
  background: #eee;
  cursor: not-allowed;
}
input~input{
  margin-top: 5px;
}
.show-info{
  white-space: pre-wrap;
  text-align: left;
}
.valid-reg{
  padding: 5px;
  font-size: 16px;
  line-height: 1.2;
  border-radius: 5px;
  border: 1px solid transparent;
}
.error:focus-within{
  border-color: red;
}
.pass:focus-within{
  border-color: green;
}
</style>
<script>
  export default {
    data() {
      return {
        value: '',
        readonly: true,
        flags: '',
        rege: '',
        exp:null
      }
    },
    props: {
      reg: [String],
      showInfo: [Boolean],
      showStep: [Boolean],
      readOnly: [Boolean]
    },
    computed: {
      valid(){
        if(this.value === "" || this.exp === null) return null
        return this.exp.test(this.value)
      },
      info(){
        if(this.showInfo && this.valid){
          return JSON.stringify(this.exp.exec(this.value), function(k,v){
            if(v && v.length && v.splice){
              return Object.assign({}, v)
            }
            return v
          },4)
        }
        return ""
      },
      // steps(){
      //   if(this.info){
      //     this.value.replace(this.exp,function(){
      //       console.log('***',arguments)
      //     })
      //   }
      // }
    },
    methods: {
      initReg(){
        if (this.reg === "") return this.exp = null;
          try{
            this.exp = new RegExp(this.rege,this.flags)
          }catch(e){
            this.exp = null
          }
      }
    },
    created(){
      this.readonly = this.readOnly
      this.rege = this.reg
      this.initReg()
    },
    watch: {
      rege(n){
        this.initReg()
        this.$emit('update:reg',n)
      },
      flags(){
        this.initReg()
      }
    }
  }
</script>
