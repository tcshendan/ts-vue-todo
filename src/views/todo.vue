<template>
  <div class="todo-page">
    <ul>
      <todo-item
        v-for="(item, index) in list"
        :key="`todo_item_${index}`"
        :item="item"
        :index="index"
        :editting-index="edittingIndex"
        @on-edit="handleEdit"
        @on-save="handleSave"
        @on-cancel="handleCancel"
        @on-complete="handleComplete"
      ></todo-item>
    </ul>
    <a-button @click="turn">跳转</a-button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import TodoItem from '../components/todo-item';
import { State, Mutation } from 'vuex-class';

@Component({
  name: 'TodoPage',
  components: {
    TodoItem,
  },
})
export default class TodoPage extends Vue {
  @State('todoList') public list;
  public edittingIndex = -1;
  // public list = [
  //   {
  //     text: '学习《TypeScript全面解读》',
  //     complete: false,
  //   },
  //   {
  //     text: '学习《Vue技术栈开发实战》',
  //     complete: false,
  //   },
  // ];
  @Mutation('updateTodoList') public updateList;
  @Mutation('todoItemComplete') public handleComplete;
  public handleSave({ index, content }) {
    // this.list[index].text = content;
    this.updateList({ index, content });
    this.handleCancel();
  }
  public handleEdit(index) {
    this.edittingIndex = index;
  }
  public handleCancel() {
    this.edittingIndex = -1;
  }
  // public handleComplete(index) {
  //   this.list[index].complete = true;
  // }
  public turn() {
    this.$router.push({
      name: 'show',
    });
  }
}
</script>
