<template>
  <div class="row">
    <div
      class="col-4 mb-4"
      v-for="column in columnList"
      :key="column.id"
    >
      <div
        class="card h-100 shadow-sm"
        style="width: 18rem;"
      >
        <div class="card-body text-center">
          <img
            :src="column.avatar"
            class="rounded-circle border border-light w-25 my-3"
            :alt="column.title"
          >
          <h5 class="card-title">{{column.title}}</h5>
          <p class="card-text text-left">{{column.discription}}</p>
          <a
            href="#"
            class="btn btn-outline-primary"
          >进入专栏</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang='ts'>
import { computed, defineComponent, PropType } from 'vue'
export interface ColumnProps {
  id: number;
  title: string;
  avatar?: string;
  discription: string;
}
export default defineComponent({
  name: 'ColumnList',
  props: {
    list: {
      // as 类型断言 不能直接写 因为 Array是一个数组的构造函数，不是个类型，无法把它断言成类型，
      // PropType解决了这个问题  它接受一个泛型 可以将Array的构造函数返回传入的泛型类型 以后想把一个构造函数断言成一个泛型 就可以用这个
      type: Array as PropType<ColumnProps[]>,
      required: true
    }
  },
  setup (props) {
    const columnList = computed(() => {
      return props.list.map((item) => {
        if (!item.avatar) item.avatar = require('@/assets/logo.png')
        return item
      })
    })
    return {
      columnList
    }
  }
})
</script>

<style>
</style>
