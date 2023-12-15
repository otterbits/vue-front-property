<template>
    <div class="discount">
    <h4>지금 결제하면 {{ 문구 }}% 할인</h4>
  </div>
</template>

<script>
export default {
    name: 'Discount',
    data(){
    return {
      문구 : 30,
    };
  },

    mounted() {
      const interVaild = setInterval(() => {
        this.문구--;
        if (this.문구 === 0) {
          clearInterval(interVaild);
        }
      }, 1000);
    }
  }

</script>

<style>

</style>