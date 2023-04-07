<template>
  <div class="todo">
    <h1>Todo List</h1>
    <div class="add-form">
      <input type="text" v-model="msg"/>
      <button @click="create()">Add</button>
    </div>
    <ul>
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :text="todo.text"
        :completed="todo.completed"
        @delete="onDelete(todo.id)"
        @check-change="onChange(todo.id)"
      />
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
import TodoItem from "./components/TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
  setup() {
    const msg = ref('');
    const id = ref(3);
    const dummyData = ref([
      { id: 1, text: "Buy milk", completed: false },
      { id: 2, text: "Do laundry", completed: true },
      { id: 3, text: "Clean room", completed: false },
    ]);

    const create = () => {
      const newItem = {
        id: ++id.value,
        text: msg.value,
        completed: false
      }

      dummyData.value.push(newItem);
      msg.value = '';
    };

    const onDelete = (id) => {
      dummyData.value = dummyData.value.filter(item => item.id != id);
    };
    
    const onChange = (idx) => {
      const changed = dummyData.value.find(item => item.id == idx);
      changed.completed = !changed.completed;
    }

    return {
      todos: dummyData,
      create,
      onDelete,
      onChange,
      msg,
      id
    };
  },
};
</script>