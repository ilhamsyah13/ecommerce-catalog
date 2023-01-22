<script setup>
import { ref } from "vue";
let cloth = ref(null);
let count = ref(0);
let category = ref("men's clothing");
let iscloth = true;

function counter() {
  count.value++;
  if (count.value > cloth.value.length - 1) {
    count.value = 0;
  } else {
    clothApi(count.value);
  }
}

async function gender() {
  if (cloth.value[count.value].category === "men's clothing") {
    category.value = "women's clothing";
  } else {
    category.value = "men's clothing";
  }
  iscloth = !iscloth;
  count.value = 0;
  await clothApi();
}

async function clothApi() {
  const res = await fetch(
    `https://fakestoreapi.com/products/category/${category.value}`
  );
  const data = await res.json();
  cloth.value = data;
}
await clothApi();
</script>

<template>
  <div class="container" v-if="cloth">
    <div class="left">
      <img :src="cloth[count].image" alt="cloth" class="img-container" />
    </div>

    <div class="right">
      <h1 :class="[iscloth ? 'title men' : 'title women']">
        {{ cloth[count].title }}
      </h1>
      <div class="categories">
        <p @click="gender" class="gender">{{ cloth[count].category }}</p>
        <p>{{ cloth[count].rating.rate }}/5</p>
      </div>
      <p class="desc">
        {{ cloth[count].description }}
      </p>
      <h4 :class="[iscloth ? 'price men' : 'price women']">
        ${{ cloth[count].price }}
      </h4>
      <div class="buttons">
        <button :class="[iscloth ? 'btn men-btn' : 'btn women-btn']">
          Buy now
        </button>
        <button
          :class="[iscloth ? 'btn men-next' : 'btn women-next']"
          @click="counter"
        >
          Next product
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  color: black;
  font-weight: 400;
  display: grid;
  grid-template-columns: 400px 1fr;
  border-radius: 10px;
  background-color: #ffffff;
  box-shadow: 1px 1px 50px -5px rgba(0, 0, 0, 0.75);
}
.men {
  color: #002772;
}
.women {
  color: #3f3f3f;
}
.img-container {
  height: 500px;
  width: 100%;
  padding: 50px;
  border-radius: inherit;
  overflow: hidden;
}
.right {
  padding: 25px;
  max-width: 600px;
}
.title {
  font-weight: 600;
}
.gender:hover {
  cursor: pointer;
  background-color: #002772;
  color: #ffffff;
  padding: 5px 10px;
  border-radius: 10px;
}
.categories {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #dcdcdc;
}
.desc {
  margin-top: 10px;
  min-height: 30%;
  border-bottom: 1px solid #dcdcdc;
}
.price {
  margin-top: 10px;
  font-weight: 600;
  font-size: 2rem;
}
.buttons {
  margin-top: 10px;
  gap: 10px;
  display: flex;
  justify-content: center;
}
.btn {
  width: 50%;
  font-family: "Inter", sans-serif;
  padding: 5px;
  border-radius: 5px;
  cursor: pointer;
}
.men-btn {
  background-color: #002772;
  color: #ffffff;
  border-color: #002772;
}
.women-btn {
  background-color: #3f3f3f;
  color: #ffffff;
  border-color: #3f3f3f;
}
.men-next {
  background-color: #ffffff;
  color: #002772;
  border-color: #002772;
}
.women-next {
  background-color: #ffffff;
  color: #3f3f3f;
  border-color: #3f3f3f;
}
.men-btn:hover {
  background-color: #ffffff;
  color: #002772;
  border-color: #002772;
}
.women-btn:hover {
  background-color: #ffffff;
  color: #3f3f3f;
  border-color: #3f3f3f;
}
.men-next:hover {
  background-color: #002772;
  color: #ffffff;
  border-color: #002772;
}
.women-next:hover {
  background-color: #3f3f3f;
  color: #ffffff;
  border-color: #3f3f3f;
}
@media (max-width: 1024px) {
  .container {
    display: block;
    margin: 20px;
    font-size: 15px;
  }
  .img-container {
    height: 200px;
    width: 100%;
    padding: 10px;
    border-radius: inherit;
    overflow: hidden;
  }
  .left {
    width: 40%;
    margin: 0 auto;
    border-radius: inherit;
    overflow: hidden;
  }
  .desc {
    margin-top: 10px;
    border-bottom: 1px solid #dcdcdc;
  }
  .price {
    padding-top: 5px;
    font-weight: 600;
    font-size: 20px;
  }
}
</style>
