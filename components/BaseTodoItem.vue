<template>
  <div
    class="BaseTodoItem"
    :class="{ 'BaseTodoItem--completed': item.completedAt }"
  >
    <div class="BaseTodoItem__checkbox">
      <slot name="checkbox">
        <input
          type="checkbox"
          disabled
          :checked="!!item.completedAt"
        >
      </slot>
    </div>
    <div class="BaseTodoItem__content">
      <slot name="content">
        {{ item.content }}
      </slot>
    </div>
    <div class="BaseTodoItem__actions">
      <slot name="actions" />
    </div>
  </div>
</template>

<script>
/**
 * @module BaseTodoItem
 */
export default {
  name: 'BaseTodoItem',
  props: {
    item: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.BaseTodoItem {
	 display: flex;
	 align-items: center;
	 margin-bottom: 1rem;
	 /* background: #fff; */
	 padding: 0.5rem;
	 border-radius: 5px;
}
 .BaseTodoItem--completed {
	 text-decoration: line-through;
	 opacity: 0.5;
}
 .BaseTodoItem__content {
	 flex: 1 1 auto;
	 padding: 0 1rem;
}
 .BaseTodoItem__actions {
	 display: flex;
	 align-items: center;
	 justify-content: center;
}
</style>
