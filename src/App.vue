<template>
  <div class="wrap"> 
    <div class="search">
   <search_by_name 
 @search-name-app="updateSearch"
 @update-page="updateNewPage"
/>
 </div> 
<div class="category">
  <category_products
  @change-category="changeCategory"
  :options="categories"
    />
</div>

    <div class="catalog"> 
     <shablon_product
        v-for="product in filteredList"
        :key="product.id"
        :product_data="product"
        @addToCartCatalog="addItemToCart"/>
    </div>
   
    
    <div class="pagination">
      <pagination_products 
        @ChangePage="onPageChange" 
        :totalSize='products.length' 
        :currentPage="curr_Page"
        :perPage="per_Page"
       
        />
  </div>
    </div>
</template>
<script>
import shablon_product from "./components/shablon_product.vue";
import pagination_products from "./components/pagination_products.vue";
import search_by_name from "./components/search_by_name.vue";
import category_products from "./components/category_products.vue";
export default {
  name: "App",
components: { shablon_product, 
pagination_products,search_by_name, category_products

  },
  data() {
    return {
      categories:['all','male','female'],
      currentCategory:'all',

      search_result:'',
      sorted_product:'',
      updatePage:{},
      total_Size:5,
      curr_Page:1,
      per_Page:4,
      products: [ 
        {name: "adidas",
          cost: "$225",
          color:"yellow",
          size:"l",
          image:'m1.jpg',
          availability:true,
          category:"male",
          id:1
        },
        {
          name: "nike",
          cost: "$335", 
          color:"green",
          size:"m",
          image:'m2.jpg',
          availability:true,
           category:"male",
          id:2
        },
        {
          name: "puma",
          cost: "$125",
          color:"yellow",
          size:"l",
          image:'m3.jpg',
          availability:true,
           category:"male",
          id:3
        },
         {
          name: "adidas ice",
          cost: "$300",
          color:"red",
          size:"s",
          image:'m4.jpg',
          availability:true,
           category:"male",
          id:4
        },
        {
          name: "T-shirt 5",
          cost: "$200",
          color:"black",
          size:"xl",
          image:'m5.jpg',
          availability:true,
           category:"male",
          id:5
        },
        {
          name: "T-shirt 6",
          cost: "$180",
          color:"blue",
          size:"xs",
          image:'m6.jpg',
          availability:true,
           category:"male",
          id:6
        },
       {
          name: "T-shirt 7",
          cost: "$192",
          color:"orange",
          size:"xl",
          image:'m7.jpg',
          availability:true,
           category:"male",
          id:7
        },
        {
          name: "T-shirt 8",
          cost: "$109",
          color:"dark grey",
          size:"m",
          image:'m8.jpg',
          availability:true,
           category:"male",
          id:8
        },
        {
          name: "T-shirt 9",
          cost: "$325",
          color:"purple",
          size:"s",
          image:'m9.jpg',
          availability:true,
          category:"male",
          id:9
        },
         {
          name: "T-shirt 10",
          cost: "$335",
          color:"orange",
          size:"xl",
          image:'u1.jpg',
          availability:true,
           category:"male",
          id:10
          },
        {
          name: "T-shirt 11",
          cost: "$299",
          color:"gray",
          size:"s",
          image:'u2.jpg',
          availability:true,
           category:"male",
          id:11
        },
        {
          name: "T-shirt 12",
          cost: "$199",
          color:"pink",
          size:"xl",
          image:'u3.jpg',
          availability:true,
          category:"male",
          id:12
        },
         {
          name: "T-shirt 13",
          cost: "$99",
          color:"yellow",
          size:"xxl",
          image:'w1.jpg',
          availability:true,
          category:"female",
          id:13
        },
       {
          name: "T-shirt 14",
          cost: "$220",
          color:"red",
          size:"xl",
          image:'w2.jpg',
          availability:true,
          category:"female",
          id:14
        },
        {
          name: "T-shirt 15",
          cost: "$300",
          color:"navy",
          size:"xs",
          image:'w3.jpg',
          availability:true,
          category:"female",
          id:15
        },
        {
          name: "T-shirt 16",
          cost: "$118",
          color:"yellow",
          size:"l",
          image:'w4.jpg',
          availability:true,
          category:"female",
          id:16
        },
         {
          name: "T-shirt 17",
          cost: "$305",
          color:"brown",
          size:"m",
          image:'w5.jpg',
          availability:true,
          category:"female",
          id:17
        },
        {
          name: "T-shirt 18",
          cost: "$301",
          color:"orange",
          size:"m",
          image:'w6.jpg',
          availability:true,
          category:"female",
          id:18
        },
        {
          name: "T-shirt 19",
          cost: "$202",
          color:"black",
          size:"s",
          image:'w7.jpg',
          availability:true,
          category:"female",
          id:19
        },
        {
          name: "T-shirt 20",
          cost: "$265",
          color:"black",
          size:"m",
          image:'w8.jpg',
          availability:true,
          category:"female",
          id:20
        },
        {
          name: "T-shirt 21",
          cost: "$265",
          color:"black",
          size:"m",
          image:'w9.jpg',
         category:"female",
          availability:true,
          id:21
        },
        {
          name: "T-shirt 22",
          cost: "$265",
          color:"black",
          size:"m",
          image:'w10.jpg',
         category:"female",
          availability:true,
          id:22
        },
        {
          name: "T-shirt 23",
          cost: "$265",
          color:"black",
          size:"m",
          image:'w11.jpg',
         category:"female",
          availability:true,
          id:23
        }
      ]
    };
  },
  methods: {
    changeCategory(item){
     this.currentCategory = item
    },

        onPageChange(page) {
            this.curr_Page=page
        },
         updateSearch(newValue){
    this.search_result = newValue      
  },
    addItemToCart(product) {
      this.$emit("addItemToCart", product);
    },
    updateNewPage(newValue){
      this.curr_Page=newValue.page;
    }
 },
computed:{
  filteredList(){
      return this.searchList.slice((this.curr_Page-1)*this.per_Page,this.curr_Page*this.per_Page)
    },
    searchList() {
      return this.products.filter(product => {
        return product.name.toLowerCase().indexOf(this.search_result.toLowerCase())!=-1 
      })
},
filteredProducts(){
  if(this.sorted_product.length){
    return this.sorted_product
  }
   return this.products
  
},
filteredByCategory(){
  if (this.currentCategory === 'all')
  return this.products 
  return this.products.filter(product => {
        return product.category === this.currentCategory
      }  
      
      )
}
},
 
}
</script>
<style>
body {
  margin: 0;
}
.wrap{
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.products{
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.products button {
  padding: 10px;
  background-color: black;
  color: white;
  outline: none;
  border: none;
  cursor: pointer;

}
.pagination{
  display:flex;
  justify-content: center;
  margin: 20px;
  margin:0 auto;
  };
  
  .Catalog{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
  padding-top: 50px;
}
.search{
  display: flex;
  justify-content: flex-start;
  margin: 10px;
}
h2{
text-align: center;
}

</style>
}
