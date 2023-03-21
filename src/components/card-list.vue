<template>
  <div class="infomation">
    <div
      class="card"
      v-for="(item, index) in cardList"
      :key="item.index"
    >
      <h2 class="card-title">
        <span contenteditable>{{ item.name }}</span>
        <button
          class="add"
          @click="handleAdd({
          name: item.name
        })"
        >+</button>
        <button
          class="delete"
          @click="handleDelete({
            card: item.name,
            num: 0
          })"
        >+</button>
      </h2>
      <!-- 插槽 -->
      <slot :name="item.slotname"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'card-list',
  props: {
    cardList: {
      type: Array,
      default: () => ([])
    }
  },
  data () {
    return {
      title: '测试'
    }
  },
  methods: {

  }
}
</script>