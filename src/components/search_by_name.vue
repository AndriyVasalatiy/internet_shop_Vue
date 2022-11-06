<template>
  <div class=searchBlock>
    <input v-model="searchValue" 
    placeholder="type name..." type="text" class="search"/>
<button class="buttonFilter"
 @click="search"> search </button>
  </div>
</template>
<script>
export default {
  name: "search_by_name",
  created() {},
  data() {
    return {
      searchValue:''
    };
  },
  methods: {
    search(){
      this.$emit("search-name-app",this.searchValue);
      this.$emit("update-page",{page:1});
      console.log(this.searchValue)
    }
  },
  computed(){}
  }
</script>
<style>
.search{
  width:100%;
}
.buttonFilter{
   width:100%;
}
.searchBlock{
  display:flex;
  flex-direction: column;
  width: 100px;
}
</style>         