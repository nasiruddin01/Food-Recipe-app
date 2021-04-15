<template>
  <div class="container">
    <div class="text">
      <h1>
        Let's start <br />
        cooking with <br />
        popular recipes
      </h1>
      <p class="text-primary">Want to learn cook but confused how to start</p>
      <p class="text-secondary">No need to worry again!</p>
      <button class="btn">Get started</button>
    </div>
    <div class="image">
      <img
        src="https://www.themealdb.com/images/media/meals/1529444113.jpg"
        alt=""
      />
    </div>
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
  display: grid;
  grid-template-columns: 1fr auto;
  grid-gap: 2rem;
  font-family: $font-primary;
  @media (max-width: 768px) {
    width: 95%;
    margin: 0 auto;
    display: grid;
    grid-template-rows: 1fr 1fr;
    grid-gap: 1rem;
  }
  .text {
    h1 {
      font-size: 4rem;
      color: #ffa36c;
      @media (max-width: 1024px) {
        font-size: 2rem;
      }
    }
    .text-primary {
      font-size: 20px;
      margin-top: 1rem;
    }
    .text-secondary {
      font-size: 16px;
      margin-top: 0.5rem;
    }
    .btn {
      margin-top: 2rem;
      padding: 0.5rem 2rem;
      background: #31b668;
      color: $color-tertiary-font;
      border: none;
      outline: none;
      border-radius: 3px;
    }
    .btn:hover {
      background: $color-tertiary-font;
      color: #31b668;
    }
  }
  .image {
    width: 30rem;
    height: 30rem;

    img {
      width: 100%;
      height: 100%;
      border: 5px solid #ffa36c;
      border-radius: 50%;
    }
  }
}
</style>
