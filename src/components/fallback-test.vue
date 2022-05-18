<template>
  <Suspense timeout="0">
    <template #default>
      <div v-for="item in articleList" :key="item.id">
        <article>
          <h2>{{ item.title }}</h2>
          <p>{{ item.body }}</p>
        </article>
      </div>
    </template>
    <template #fallback>
      <div>
        <h1>
          <!-- this is not displaying, don't know why -->
          Articles loading...
        </h1>
      </div>
    </template>
  </Suspense>
</template>
<script>
import axios from 'axios'
// import { computed, ref, watch, watchEffect } from "vue";
// import { watch } from 'vue'
export default {
  async setup() {

    const wait = (timeToDelay) => {
      return new Promise((resolve) => {
        console.log(resolve, "done")
        setTimeout(resolve, timeToDelay)
      })
    }

    let articleList = await axios
      .get('https://jsonplaceholder.typicode.com/posts')
      .then(async (response) => {
        
        /* 
          정리:
          axios 는 promise를 return. 즉 then 안에있는거는 callback function이기 때문에, 
          callback function 자체에도 비동기를 걸어줘야한다. 
          즉, async, await을 설정해줘야 한다.
        
        */

        await wait(10000)
        // await setTimeout(resolve, 3000)
        return response.data
      })

    return {
      articleList
    }
  }
}
</script>