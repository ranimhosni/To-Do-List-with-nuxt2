
<template>
  <div>
    <TodoList />
  </div>
</template>
<style>
*{
    background : #512985;
}
</style>
<script>
import TodoList from "@/components/To-Do-List.vue";

export default {
  components: {
    TodoList
  }
};
</script>