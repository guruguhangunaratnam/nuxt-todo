<template>
  <base-todo-item
    class="TodoItem"
    :item="item"
  >
    <template #checkbox>
      <input
        v-model="completedLocal"
        type="checkbox"
        class="checkbox"
        data-testid="completeCheckbox"
      >
    </template>
    <template #content>
      <div
        v-if="!isEditing"
        class="break-all"
        data-testid="contentEditTrigger"
        @dblclick="enableEdit"
      >
        {{ item.content }}
      </div>
      <input
        v-if="isEditing"
        ref="editInput"
        v-model="contentLocal"
        type="text"
        class="input"
        data-testid="editInput"
        @keyup.enter="saveEdit"
        @blur="saveEdit"
        @keyup.esc="stopEdit"
      >
    </template>
    <template #actions>
      <button
        class="TodoItem__delete button is-inverted is-danger is-small"
        data-testid="deleteTrigger"
        @click.prevent="deleteItem"
      >
        <span class="icon"><svg width="1.33em" height="1.33em" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg" fill="#f56565"><path d="M704 1376v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm256 0v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm256 0v-704q0-14-9-23t-23-9h-64q-14 0-23 9t-9 23v704q0 14 9 23t23 9h64q14 0 23-9t9-23zm-544-992h448l-48-117q-7-9-17-11h-317q-10 2-17 11zm928 32v64q0 14-9 23t-23 9h-96v948q0 83-47 143.5t-113 60.5h-832q-66 0-113-58.5t-47-141.5v-952h-96q-14 0-23-9t-9-23v-64q0-14 9-23t23-9h309l70-167q15-37 54-63t79-26h320q40 0 79 26t54 63l70 167h309q14 0 23 9t9 23z"/></svg></span>
      </button>
      <div class="TodoItem__reorderHandle">
        <svg width="1.33em" height="1.33em" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg" fill="#333333"><path d="M1664 1344v128q0 26-19 45t-45 19h-1408q-26 0-45-19t-19-45v-128q0-26 19-45t45-19h1408q26 0 45 19t19 45zm0-512v128q0 26-19 45t-45 19h-1408q-26 0-45-19t-19-45v-128q0-26 19-45t45-19h1408q26 0 45 19t19 45zm0-512v128q0 26-19 45t-45 19h-1408q-26 0-45-19t-19-45v-128q0-26 19-45t45-19h1408q26 0 45 19t19 45z"/></svg>
      </div>
    </template>
  </base-todo-item>
</template>

<script>
import BaseTodoItem from '@/components/BaseTodoItem'

/**
 * @module TodoItem
 */
export default {
  name: 'TodoItem',
  components: { BaseTodoItem },
  props: {
    /**
     *  @type TodoItem
     */
    item: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      isEditing: false,
      contentLocal: ''
    }
  },
  computed: {
    completedLocal: {
      /**
       * Transforms the completedAt timestamp to boolean
       */
      get () {
        return !!this.item.completedAt
      },
      /**
       * Converts the completedAt boolean to a timestamp
       * Emits the entire changed item
       * @param {Boolean} value
       */
      set (value) {
        this.emitChange({
          completedAt: value ? Date.now() : null
        })
      }
    }
  },
  methods: {
    /**
     * Deletes a todo item
     */
    deleteItem () {
      this.emitChange({
        deletedAt: Date.now()
      })
    },
    /**
     * Emits the changes to the TODO item up to the parent.
     * @param {Object} updatedItem - the todo item
     */
    emitChange (updatedItem) {
      this.$emit('change', {
        ...this.item,
        ...updatedItem
      })
    },
    /**
     * Starts the editing of a todo item.
     * Focuses the input item immediately
     * @return {Promise<void>}
     */
    async enableEdit () {
      this.contentLocal = this.item.content
      this.isEditing = true
      await this.$nextTick()
      this.$refs.editInput.focus()
    },
    /**
     * Saves the editing changes.
     * If no content is provided, just closes
     */
    saveEdit () {
      if (this.contentLocal) {
        this.emitChange({
          content: this.contentLocal
        })
      }
      this.stopEdit()
    },
    /**
     * Stops the editing, without saving anything
     */
    stopEdit () {
      this.isEditing = false
      this.contentLocal = ''
    }
  }
}
</script>

<style scoped>
.TodoItem:hover .TodoItem__delete {
	 opacity: 1;
}
 .TodoItem__delete {
	 opacity: 0;
	 margin-right: 0.5rem;
	 border-radius: 100%;
}
 .TodoItem__reorderHandle:hover {
	 cursor: grab;
}
 .TodoItem__reorderHandle:active {
	 cursor: grabbing;
}
 
</style>
