<template>
  <div class="">
    <ShoppingCart 
      v-if="contentData" class="stick-to-screen"
      :data="contentData" :itemCount="itemCount" :showCart="showCart"
      @update="update" @toggleCart="toggleCart">
    </ShoppingCart>
    <div v-show="showCart" class="overlay"></div>

    <img class="logo" src="https://drive.google.com/uc?export=view&id=1B15rl0EX-19tRhuMG0-KWn3vwn7CRybo">
    <StoreItems 
      v-if="contentData"
      :data="contentData" @update="update">
    </StoreItems>
  </div>
</template>

<script>
import ShoppingCart from '@/components/ShoppingCart.vue'
import StoreItems from '@/components/StoreItems.vue'
import content from '@/data/data.json'

export default {
  components: {
    ShoppingCart,
    StoreItems
  },

  data() {
    return {
      content,
      contentData: [],
      itemCount: 0,
      showCart: false
    }
  },

  beforeMount() {
    this.getContentInfo()
  },

  methods: {
    getContentInfo(){
      // Pretend GET request
      this.contentData = content
    },

    update(newData){
      this.data = newData
      this.recountInventory()
    },

    toggleCart(){
      this.showCart = !this.showCart
    },

    recountInventory(){
      let itemCount = 0
      let tempData = this.data
      for(let index in tempData){
        itemCount = (itemCount + tempData[index].quantity)
      }
      this.itemCount = itemCount
    }
  }
}
</script>

<style>
  .container {
    position: relative;
  }

  .overlay {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    content: " ";
    background: rgba(0, 0, 0, 0.25);
    z-index: 5;
  }

  .stick-to-screen {
    position: fixed;
    top: 40px;
    z-index: 10;
  }

  .logo {
    display: block;
    margin: 0px auto;
    height: auto;
    width: 300px;
  }
</style>
