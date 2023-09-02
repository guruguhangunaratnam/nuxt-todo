<template>
  <base-todo-item
    class="RecycledTodoItem text-left"
    :item="item"
  >
    <template #actions>
      <div class="buttons">
        <button
          title="Restore from Trash"
          data-testid="restoreTrigger"
          @click="$emit('restore', item)"
        >
          <span class="icon">
            <svg width="1.33em" height="1.33em" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg" fill="#4299e1"><path d="M1664 896q0 156-61 298t-164 245-245 164-298 61q-172 0-327-72.5t-264-204.5q-7-10-6.5-22.5t8.5-20.5l137-138q10-9 25-9 16 2 23 12 73 95 179 147t225 52q104 0 198.5-40.5t163.5-109.5 109.5-163.5 40.5-198.5-40.5-198.5-109.5-163.5-163.5-109.5-198.5-40.5q-98 0-188 35.5t-160 101.5l137 138q31 30 14 69-17 40-59 40h-448q-26 0-45-19t-19-45v-448q0-42 40-59 39-17 69 14l130 129q107-101 244.5-156.5t284.5-55.5q156 0 298 61t245 164 164 245 61 298zm-640-288v448q0 14-9 23t-23 9h-320q-14 0-23-9t-9-23v-64q0-14 9-23t23-9h224v-352q0-14 9-23t23-9h64q14 0 23 9t9 23z"/></svg>
          </span>
        </button>
        <button
          title="Remove from Recycle Bin"
          data-testid="removeTrigger"
          @click="$emit('remove', item)"
        >
          <span class="icon">
            <svg width="1.33em" height="1.33em" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg" fill="#333333"><path d="M704 1376v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm256 0v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm256 0v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm-544-992h448l-48-117q-7-9-17-11h-317q-10 2-17 11zm928 32v64q0 14-9 23t-23 9h-96v948q0 83-47 143.5t-113 60.5h-832q-66 0-113-58.5t-47-141.5v-952h-96q-14 0-23-9t-9-23v-64q0-14 9-23t23-9h309l70-167q15-37 54-63t79-26h320q40 0 79 26t54 63l70 167h309q14 0 23 9t9 23z"/></svg>
          </span>
        </button>
      </div>
    </template>
  </base-todo-item>
</template>

<script>
import BaseTodoItem from '@/components/BaseTodoItem'

/**
 * @module RecycledTodoItem
 */
export default {
  name: 'RecycledTodoItem',
  components: { BaseTodoItem },
  props: {
    item: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.RecycledTodoItem .buttons {
  flex-wrap: nowrap;
}
</style>
