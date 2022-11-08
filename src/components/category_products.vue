<template>
<div>
<div v-for="item in options" 
  :key="item" >
    <input
      type="radio"
      :value="item"
      name="option"
      @change="ChangeChoose(item)"
    >
    <label :for="item">{{item}}</label>
    </div>
    </div>
</template>

<script>
export default {
  name: "category_products",
  created() {},
  data() {
    return {
      categoryArr:[]
    };
  },
  props: {
    options:{
      type: Array
      }
    },
  methods: {
  ChangeChoose(item){
    this.$emit('change-category',item);
  },
mounted(){
   this.ChangeChoose()
}
}
}
</script>

<style>

.options{
  border:solid 1px #aeaeae;
  position:absolute;
  top:20 px;
  right:0;
  width:100%;
}
.select{
  position:relative;
  width:200px;
}
.select p{
  margin:0;
}
.title{
  border:solid 1px red;
}
</style>