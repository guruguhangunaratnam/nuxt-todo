<template>
  <div class="RecycleBin">
    <div class="text-xs text-right text-gray-500 uppercase pr-6">
      Deleted Items
    </div>
    <div class="RecycleBin__content">
      <div
        v-if="deletedItems.length"
        class="RecycleBin__items pt-3 px-3"
      >
        <recycled-todo-item
          v-for="item in deletedItems"
          :key="item.id"
          :item="item"
          @remove="removeFromBin"
          @restore="restore"
        />
      </div>
      <div
        v-else
        style="margin-left:auto; margin-right:auto;"
      >
        <div style="width:100%">
          <div style="width:75px; margin-left: auto; margin-right:auto">
        <svg width="75" height="75" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg" fill="#cccccc"><path d="M704 1376v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm256 0v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm256 0v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm-544-992h448l-48-117q-7-9-17-11h-317q-10 2-17 11zm928 32v64q0 14-9 23t-23 9h-96v948q0 83-47 143.5t-113 60.5h-832q-66 0-113-58.5t-47-141.5v-952h-96q-14 0-23-9t-9-23v-64q0-14 9-23t23-9h309l70-167q15-37 54-63t79-26h320q40 0 79 26t54 63l70 167h309q14 0 23 9t9 23z"/></svg>
        </div>
                  <div class="pt-2">the recycling bin is empty</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ToDoService } from '@/plugins/ToDoService'
import RecycledTodoItem from '@/components/RecycledTodoItem'

/**
 * @module RecycleBin
 */
export default {
  name: 'RecycleBin',
  components: { RecycledTodoItem },
  data () {
    return {
      deletedItems: []
    }
  },
  mounted () {
    this.fetchDeletedItems()
  },
  methods: {
    /**
     * Fetches the list of deleted todo items
     */
    fetchDeletedItems () {
      this.deletedItems = ToDoService.fetchDeleted()
    },
    /**
     * Restores a todo item from the recycling bin
     * @param {TodoItem} item
     */
    restore (item) {
      item.deletedAt = null
      ToDoService.updateItem(item.id, item)
      this.fetchDeletedItems()
    },
    removeFromBin (item) {
      ToDoService.removeItem(item.id)
      this.fetchDeletedItems()
    }
  }
}
</script>
