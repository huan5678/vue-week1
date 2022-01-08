<template>
  <main class="container">
    <div class="flex flex-wrap lg:flex-nowrap justify-around py-4 gap-4">
      <section class="lg:w-1/2">
        <h2 class="text-h2 font-medium mb-8">產品列表</h2>
        <table class="table-auto w-full mb-4">
          <thead class="border-b-2 border-black">
            <tr>
              <td width="200" class="pb-2 font-bold whitespace-nowrap">
                產品名稱
              </td>
              <td width="250" class="pb-2 font-bold whitespace-nowrap">原價</td>
              <td width="250" class="pb-2 font-bold whitespace-nowrap">售價</td>
              <td width="250" class="pb-2 font-bold whitespace-nowrap">
                是否啟用
              </td>
              <td width="150" class="pb-2 font-bold whitespace-nowrap">
                查看細節
              </td>
            </tr>
          </thead>
          <tbody>
            <tr
              class="border-b border-gray-300 hover:bg-gray-200"
              v-for="item in products"
              :key="item.id"
            >
              <td class="py-2 whitespace-nowrap">{{ item.title }}</td>
              <td class="py-2 whitespace-nowrap">{{ item.origin_price }}</td>
              <td class="py-2 whitespace-nowrap">{{ item.price }}</td>
              <td
                class="py-2 whitespace-nowrap text-green-700"
                v-if="item.is_enabled === 1"
              >
                啟用
              </td>
              <td class="py-2 whitespace-nowrap text-gray-400" v-else>
                未啟用
              </td>
              <td class="py-2 whitespace-nowrap">
                <button
                  type="button"
                  class="text-white bg-blue-500 rounded px-3 py-2 hover:bg-blue-600 transition duration-200"
                  @click="handlerGetTarget(item)"
                >
                  查看細節
                </button>
              </td>
            </tr>
          </tbody>
        </table>
        <p>目前有{{ products.length }}項產品</p>
      </section>
      <section class="lg:w-1/2">
        <div v-if="targetProduct === null">
          <p class="text-gray-400">請選擇一個商品查看</p>
        </div>
        <div v-else>
          <h1 class="text-h2 font-medium">單一產品細節</h1>
          <div
            class="border rounded flex flex-col justify-center items-center mb-4"
          >
            <img
              class="max-h-[300px]"
              :src="targetProduct?.imageUrl"
              :alt="targetProduct?.title"
            />
            <div class="p-4">
              <h2 class="font-bold text-xl mb-2">
                {{ targetProduct?.title }}
                <span
                  class="px-2 py-1 ml-2 rounded text-sm bg-blue-500 text-white"
                >
                  {{ targetProduct?.category }}
                </span>
              </h2>
              <ul class="space-y-4 pb-3">
                <li>商品描述：{{ targetProduct?.description }}</li>
                <li>商品內容：{{ targetProduct?.content }}</li>
                <li>
                  {{ targetProduct?.price }}
                  <span class="pl-1 text-gray-400 line-through">{{
                    targetProduct?.origin_price
                  }}</span>
                  個 / 元
                </li>
              </ul>
            </div>
          </div>
          <div class="px-2 flex gap-4">
            <img
              v-for="img in targetProduct?.imagesUrl"
              :key="img"
              class="max-h-32 object-cover"
              :src="img"
            />
          </div>
        </div>
      </section>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

let targetProduct = ref(null);

const products = ref([
  {
    category: "甜甜圈",
    content: "尺寸:14x14cm",
    description:
      "濃郁的草莓風味，中心填入滑順不膩口的卡士達內餡，帶來滿滿幸福感!",
    id: "-L9tH8jxVb2Ka_DYPwng",
    is_enabled: 1,
    origin_price: 150,
    price: 99,
    title: "草莓莓果夾心圈",
    unit: "個",
    num: 10,
    imageUrl:
      "https://images.unsplash.com/photo-1583182332473-b31ba08929c8?ixid=MnwxMjA3fDB8MHxzZWFyY2h8NzR8fGRvbnV0fGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=700&q=60",
    imagesUrl: [
      "https://images.unsplash.com/photo-1626094309830-abbb0c99da4a?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2832&q=80",
      "https://images.unsplash.com/photo-1559656914-a30970c1affd?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTY0fHxkb251dHxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=700&q=60",
    ],
  },
  {
    category: "蛋糕",
    content: "尺寸:6寸",
    description:
      "蜜蜂蜜蛋糕，夾層夾上酸酸甜甜的檸檬餡，清爽可口的滋味讓人口水直流!",
    id: "-McJ-VvcwfN1_Ye_NtVA",
    is_enabled: 1,
    origin_price: 1000,
    price: 900,
    title: "蜂蜜檸檬蛋糕",
    unit: "個",
    num: 1,
    imageUrl:
      "https://images.unsplash.com/photo-1627834377411-8da5f4f09de8?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1001&q=80",
    imagesUrl: [
      "https://images.unsplash.com/photo-1618888007540-2bdead974bbb?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=987&q=80",
    ],
  },
  {
    category: "蛋糕",
    content: "尺寸:6寸",
    description: "法式煎薄餅加上濃郁可可醬，呈現經典的美味及口感。",
    id: "-McJ-VyqaFlLzUMmpPpm",
    is_enabled: 1,
    origin_price: 700,
    price: 600,
    title: "暗黑千層",
    unit: "個",
    num: 15,
    imageUrl:
      "https://images.unsplash.com/photo-1505253149613-112d21d9f6a9?ixid=MnwxMjA3fDB8MHxzZWFyY2h8NDZ8fGNha2V8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=700&q=60",
    imagesUrl: [
      "https://images.unsplash.com/flagged/photo-1557234985-425e10c9d7f1?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTA5fHxjYWtlfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=700&q=60",
      "https://images.unsplash.com/photo-1540337706094-da10342c93d8?ixid=MnwxMjA3fDB8MHxzZWFyY2h8NDR8fGNha2V8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=700&q=60",
    ],
  },
]);

function handlerGetTarget(params) {
  this.targetProduct = params;
}
</script>
