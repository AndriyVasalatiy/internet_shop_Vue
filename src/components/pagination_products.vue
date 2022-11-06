<template>
    <div >
      
      <button :disabled="isButtonDisabled" @click="onChangePage(1)">First</button>
      <button :disabled="isButtonDisabledNext(this.currentPage,1)" @click="onChangePage(currentPage-1)">Prev</button>
      <button
      v-for ="page in totalPage" 
      :key="page"
      @click="onChangePage(page)"
      :class="{'active': this.curr_Page === page}">
      {{page}}
      </button> 
      <button :disabled="isButtonDisabledNext(totalPage-currentPage,0)" @click="onChangePage(currentPage+1)">Next</button>
      <button :disabled="isButtonDisabledNext(totalPage-currentPage,0)" @click="onChangePage(this.totalPage)">Last</button>

      </div>
</template>
    <script>
      export default{
        name: 'pagination_products',
        props:{
          totalSize: {
            type: Number
          },
          perPage:{
            type: Number,
          },
          currentPage:{
            type: Number
          }
        },
        methods:{
           onChangePage(atr){
            this.$emit('ChangePage',atr)
           },
           isButtonDisabledNext(attr,num){
            if(attr > num) 
            return false;
            else return true
          }
        },
        computed:{
          totalPage() {
            return Math.ceil(this.totalSize/this.perPage)
          },
          isButtonDisabled(){
            if(this.currentPage == 1)
            return true;
            else return false
           },
        },
      }
</script>
