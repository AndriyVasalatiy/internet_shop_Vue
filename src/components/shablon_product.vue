 <template>
  <div class="catalog-item">
    <img class="image"  :src="showImage">
    <div class="catalog-item__name">{{ product_data.name }}</div>
    <div class="catalog-item__price">Price: {{ product_data.cost }}  </div>
    <div class="catalog-item__name">Article:{{ product_data.id }}</div>
    <button class="v-catalog-item__add_to_cart_btn btn" @click="addToCart">
      Add to cart
    </button>
  </div>

</template>
<script>
export default {
  name:"shablon_product",
  props: {
    product_data: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  data() {
    return {};
  },
  computed: {
    showImage(){
      return require('../assets/' + this.product_data.image);
      
  }
  },
  methods: {
  addToCart() {
      this.$emit("addToCartCatalog", this.product_data.id);
      console.log('added')  
    }
  
  }
}
</script>
<style >
.catalog-item {
  display: flex;
  flex-direction: column;
  margin: 10px;
  border: 2px solid rgb(111, 111, 129);
  width:12%;
  align-items: center;
}
.image{
  width:95%;
  height:250px;
 border:1px solid grey;
  margin: 5px auto 5px auto ;

}
.v-catalog-item__add_to_cart_btn btn{
  margin-bottom: 10px;
  
}
 .catalog{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
   width:100%;
   border:1 px solid rgb(111, 111, 116);}
</style>