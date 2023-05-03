<template>
  <div class="discount">
    <h4 >지금 결제하면 {{discountRate}}% 할인</h4>
  </div>
</template>

<script>
export default {
    name: "DiscountComponent",
    props: {
      discountRate: Number,
    },
    mounted(){
      let timer = setInterval(() => {
        if(this.discountRate <= 0){
          clearInterval(timer);
        }else{
          this.$emit("decreaseRate"); 
        }
      }, 1000);
    },
}
</script>

<style>

</style>