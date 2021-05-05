<template>
  <div class="cart-container columns">
    <div v-show="showCart" class="column is-7 is-offset-4 cart is-clearfix">
      <h1 class="title">My Cart</h1>
      <hr>
      <div class="cart-items columns is-multiline">
        <div v-for="item, index in data" :key="`cart${index}_${item.id}`" 
             v-show="item.quantity > 0" class="cart-item column is-6">
             <div class="columns">
                <img class="cart-icon column is-3" :src="item.icon">
                <div class="cart-details column is-9">
                  <field class="field">
                    <label class="label">{{ item.title }} ({{ item.quantity }})</label>
                    <div class="control">
                      <button class="button is-danger" @click="removeItem(item.id)">Remove</button>
                    </div>
                  </field>
                </div>
             </div>
        </div>

        <div v-show="itemCount < 1" class="column is-12">
          <h2 class="subtitle has-text-grey has-text-centered">
              Nothing in the cart.
          </h2>
        </div>
      </div><br>

      <div class="is-pulled-right">
        <button class="button is-grey" @click="toggleShowCart">
          Close
        </button> &nbsp;
        <button class="button is-danger" @click="removeAllItems">
          Reset
        </button> &nbsp;
        <button class="button is-success" @click="doNothing">
          Checkout
        </button>
      </div>
    </div>

    <div class="column is-1" :class="{'is-offset-11': showCart === false}">
      <button class="button toggle is-white counter-container" v-on:click="toggleShowCart">
        <img src="https://drive.google.com/uc?export=view&id=1thfe_JR_0uFG8xbP2m9YfWYd5tiieuuf">
        <div v-if="itemCount > 0" class="counter has-text-centered">
          <span class="counter-content is-unselectable">
            <b>
              <span v-if="itemCount < 100">{{ itemCount }}</span>
              <span v-else>99+</span>
            </b>
          </span>
        </div>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  components: {},

  props: {
    data: {
      required: true
    },
    itemCount: {
      required: true
    },
    showCart: {
      required: true
    }
  },

  data() {
    return {
      nothingCount: 0
    }
  },

  beforeMount() {},

  methods: {
    toggleShowCart(){
      this.$emit("toggleCart")
    },

    removeItem(itemId){
      let tempData = this.data
      for(let index in tempData){
        if(tempData[index].id === itemId){
          tempData[index].quantity = 0
          break
        }
      }
      this.$emit("update", tempData)
    },

    removeAllItems(){
      let tempData = this.data
      for(let index in tempData){
          tempData[index].quantity = 0
      }
      this.$emit("update", tempData)
    },

    doNothing(){
      switch(this.nothingCount) {
        case 0:
          alert('Nothings gonna happen')
          break

        case 1:
          alert('Ok. Don\'t click anymore')
          break

        case 2:
          alert('Please stop.')
          break

        case 3:
          alert('WOW!')
          break

        default:
          alert('...')
      }
      this.nothingCount = this.nothingCount + 1
    }
  },
}
</script>

<style scoped>
  .columns {
    width: 95%;
    z-index: 100;
  }

  .cart {
    background: white;
    max-height: 80vh;
    padding: 2%;
    border-radius: 5px;
  }

  .cart .cart-items {
    height: 275px;
    overflow-y: scroll;
  }

  .cart .cart-items .cart-icon{
    border-radius: 50%;
    height: 100px;
    width: auto;
  }

  .button.toggle {
    height: 75px;
    width: 75px;
    border-radius: 50%;
    border-width: 5px !important;
    border-color: #008136 !important;
  }

  .counter-container {
    position: relative;
  }

  .counter-container .counter {
    position: absolute;
    height: 30px;
    width: 30px;
    bottom: -9px;
    right: -9px;
    color: white;
    border-radius: 50%;
    background: red;
  }

  .counter-container .counter .counter-content {
    display: block;
    margin: 0 auto;
    font-size: 13px;
    line-height: 30px;
  }

  @media screen and (max-width: 768px) {
    .cart-container {
      margin: 6% !important;
      width: 88% !important;
     }

     .cart .cart-items{
      width: 100% !important;
    }

    .cart .cart-items .cart-item{
      display: inline-block;
      height: 100px !important;
      width: 48% !important;
      margin: 1% !important;
    }

    .cart .cart-items .cart-item .columns{
      text-align: center;
      margin: 10%;
      margin-top: 0px;
      margin-bottom: 20px;
    }

    .cart .cart-items .cart-item .cart-icon {
      margin: 0 auto;
    }
  }
</style>
