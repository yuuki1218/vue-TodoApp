<template>
  <div>
    <div class="main-title">
      <h1>ToDoリスト</h1>
    </div>
    <div class="todo-area">
      <div class="radio-wrap">
        <input
          type="radio"
          id="all"
          name="status"
          value="全て"
          v-model="radioValue"
          @change="showStatus"
        /><label for="all">全て</label>
        <input
          type="radio"
          id="now"
          name="status"
          value="作業中"
          v-model="radioValue"
          @change="showStatus"
        /><label for="now">作業中</label>
        <input
          type="radio"
          id="finish"
          name="status"
          value="完了"
          v-model="radioValue"
          @change="showStatus"
        /><label for="finish">完了</label>
      </div>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
            <th>削除</th>
          </tr>
        </thead>
        <!-- 作業中・完了の表示 -->
        <tbody id="todo-lists-wrap">
          <tr v-for="(todo, index) in todos" :key="todo.comment" v-show="radioValue === todo.status">
            <td class="id">{{ index }}</td>
            <td>{{ todo.comment }}</td>
            <td class="status-value" @click="changeStatus(index)">{{ todo.status }}</td>
            <td @click="deleteComment(index)">{{ todo.deleteBtn }}</td>
          </tr>
          <!-- 全ての表示 -->
          <tr v-for="(todo, index) in todos" :key="todo.comment" v-show="radioValue === '全て'">
            <td class="id">{{ index }}</td>
            <td>{{ todo.comment }}</td>
            <td class="status-value" @click="changeStatus(index)">{{ todo.status }}</td>
            <td @click="deleteComment(index)">{{ todo.deleteBtn }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="form-wrap">
      <label for="comment"
        >コメント
        <input type="text" id="comment" name="comment" v-model="value" />
      </label>
      <button @click="addComment">送信</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: '',
      todos: [],
      radioValue: '全て',
    };
  },
  methods: {
    addComment() {
      if (!this.value) {
        alert('コメントを入力してください。');
      } else {
        const todo = {};
        todo.comment = this.value;
        (todo.status = '作業中'),
          (todo.deleteBtn = '削除'),
          this.todos.push(todo);
        this.value = '';
        this.showStatus();
      }
    },
    changeStatus(index) {
      const todo = this.todos[index];
      if (event.target.textContent === '作業中') {
        todo.status = '完了';
      } else {
        todo.status = '作業中';
      }
      this.showStatus();
      console.log(todo);
    },
    deleteComment(id) {
      this.todos.splice(id, 1);
    },
  },
};
</script>

<style scoped>
table {
  margin: 0 auto;
}

#todo-lists-wrap {
  height: 40px;
}
</style>
