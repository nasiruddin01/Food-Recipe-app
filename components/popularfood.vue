<template>
  <div class="container">
    <div class="text">
      <h1>Popular Food</h1>
      <p>
        We provide a variety of food and beverage recipes <br />
        with high test from famous chefs
      </p>
    </div>
    <div class="food-container"></div>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
@import '@/assets/style.scss';
.container {
  max-width: 1080px;
  width: 100%;
  margin: 2rem auto 0 auto;
  @media (max-width: 768px) {
    max-width: 100%;
    width: 90%;
  }
  .text {
    h1 {
      text-align: center;
      font-size: 3rem;
      font-weight: 300;
    }
    p {
      text-align: center;
      margin-top: 1rem;
      font-size: 16px;
      line-height: 20px;
      @media (max-width: 768px) {
        font-size: 12px;
        line-height: 16px;
      }
    }
  }
  .food-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
    grid-gap: 1rem;
  }
}
</style>
