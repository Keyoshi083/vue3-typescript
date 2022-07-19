<template lang="">
  <div class="container">
    <h1>最近の支出</h1>
    <input v-model="item1.name" />
    <input v-model="item1.price" />
    <!-- <input @input="input" :value="item1.name" />
    <input @input="inputPrice" :value="item1.price" /> -->
    <button @click="clear">Clear</button>
    <div class="payment">
      <!-- <label>{{ itemName1 }}</label>
      <label>{{ price1 }} yen</label> -->
      <label>{{ item1.name }}</label>
      <!-- <label>{{ priceLabel }}</label> -->
      <label>{{ priceLabelW }}</label>
      <a :href="url1">boughten at ...</a>
      <button @click="buy(item1.name)">BUY</button>
    </div>
    <div class="payment">
      <label>{{ itemName2 }}</label>
      <label>{{ price2 }} yen </label>
      <button @click="buy(itemName2)">BUY</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed, watch, toRefs, onMounted } from "vue";
//TODO:Vue3系でリアクティブ（動的）な値を用いるときはref<T>を用いる
const itemName1 = ref<string>("Desk");
const itemName2 = "Bike";

//TODO: オブジェクト形式のものに対してリアクティブな値を用いるときはreactiveメソッドを使う
const item1 = reactive({
  name: "Desk",
  price: 20000,
});

const price1 = ref<number>(20000);
const price2 = 40000;

const url1 = "https://google.com";

const buy = (itemName: string) => {
  alert(`Are you sure to buy ${itemName} ?`);
};

const budget = 50000;

//TODO:Computedコンポーネント内の値に対して条件を指定して、値を変更したい
const priceLabel = computed(() => {
  console.log("computed");
  return item1.price > budget ? "Too Expensive" : `${item1.price} yen`;
});

//TODO:Watchプロパティの書き方
let priceLabelW = ref<string>(`${item1.price} yen`);
const { price } = toRefs(item1);
/**
 * 第一引数：監視対象の変数、第二引数：実行する処理を記載した関数
 */
watch(price, () => {
  console.log("watch");
  price.value > budget
    ? (priceLabelW.value = "Too Expensive")
    : (priceLabelW.value = `${item1.price} yen`);
});

/**
 * v-modelを利用しない場合にINPUTの内容を受け取り、値を設定する関数
 * @param event InputEvent
 */
const input = (event: InputEvent) => {
  const { target } = event;
  //TODO:InputEventはtargetの型を確定させないとTypeScriptではエラーとなる
  if (!target) return;
  if (!(target instanceof HTMLInputElement)) return;
  // itemName1.value = target.value;
  item1.name = target.value;
};

/**
 * v-modelを利用しない場合にINPUTの内容を受け取り、値を設定する関数
 * @param event InputEvent
 */
const inputPrice = (event: InputEvent) => {
  const { target } = event;
  if (!target) return;
  if (!(target instanceof HTMLInputElement)) return;
  // price1.value = Number(target.value);
  item1.price = Number(target.value);
};

onMounted(() => {
  console.log("onMouted");
});

const clear = () => {
  item1.name = "";
  item1.price = 0;
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background-color: rgb(3, 26, 47);
  margin-bottom: 8px;
}

input {
  margin-bottom: 8px;
}

label {
  font-size: 20px;
  font-weight: bold;
}
</style>
