<template>
  <div class="global-background">
    <router-view/>
    <span class="add-signature"> by /arreolabenn</span>
  </div>
</template>

<style scoped>
  .global-background {
    background-image: linear-gradient(to top, #EEE , #FFF);
  }

  .add-signature {
    display: block;
    text-align: right;
    margin-top: 100px;
    padding-bottom: 15px;
    padding-right: 20px;
  }
</style>
