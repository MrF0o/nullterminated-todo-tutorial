<template>
  <li class="item">
    <div class="checkbox">
      <input
        type="checkbox"
        :checked="completed"
        @change="onChange()"
      />
    </div>
    <div :class="completed ? 'completed text' : 'text'">
      {{ text }}
    </div>
    <div class="delete" @click="onDelete()">
      <font-awesome-icon icon="fa-regular fa-trash-can" />
    </div>
  </li>
</template>

<script>
export default {
  props: {
    text: String,
    completed: Boolean,
  },
  setup(props, context) {
    const onChange = () => {
      context.emit("check-change");
    };

    const onDelete = () => {
      context.emit("delete");
    };

    return {
      onChange,
      onDelete
    };
  },
};
</script>