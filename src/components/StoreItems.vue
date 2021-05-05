<template>
  <div class="columns">
    <div class="column is-10 is-offset-1">

      <div v-if="data" class="columns is-multiline">
        <div v-for="item, index in data" :key="`store${index}_${item.id}`" class="card column is-4 custom-card">
          <div class="card-image custom-card-image">
            <figure class="image is-4by3">
              <img :src="item.src">
            </figure><br>
            <span class="title is-text-centered m-1">{{item.title}}</span>
          </div>
          <div class="card-content">
            <p class="custom-content">
              {{ item.content }}
            </p>

            <div class="custom-input-container">
                <div class="field has-addons">
                  <div class="control">
                    <input class="input" type="number" min="0" :ref="`storeInput_${item.id}`" value="0">
                  </div>
                  <div class="control">
                    <button class="button is-success" @click="addItem(item.id, `storeInput_${item.id}`)">
                      Add Me
                    </button>
                  </div>
                </div>
            </div>

          </div>
        </div>
        <ShoppingCart></ShoppingCart>
      </div>

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
  },

  data() {
    return {}
  },

  beforeMount() {},

  methods: {
    addItem(itemId, itemReference){
      let tempData = this.data
      let target = itemReference
      let inputValue = this.$refs[target].value

      if(inputValue < 0){
        inputValue = 0
        this.$refs[target].value = inputValue
      }

      for(let index in tempData){
        if(tempData[index].id === itemId){
          tempData[index].quantity = parseInt(tempData[index].quantity) + parseInt(inputValue)
          break
        }
      }
      this.$emit("update", tempData)
    },
  },

  computed: {}
}
</script>

<style scoped>
  .card-content .custom-content {
    margin-bottom: 60px;
   }

  .card-content .custom-input-container {
    position: absolute;
    border-style: none;
    font-size: 15px;
    bottom: 30px;
    color: #000;
    right: 50%;
    transform: translate(50%, 0);
  }

  .card.is-4 {
    margin: 0.25% !important;
    width: 32.8% !important;
  }

  .card-image.custom-card-image {
    padding: 10px;
  }

  .card-image.custom-card-image .image img{
    border-radius: 10px;
  }

  @media screen and (max-width: 768px) {
    .card.is-4 {
      margin: 6% !important;
      margin-top: 1% !important;
      margin-bottom: 1% !important;
      width: 88% !important;
     }
  }
</style>


