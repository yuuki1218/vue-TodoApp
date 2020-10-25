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
          value="全て"
          v-model="radioValue"
          @change="showStatus"
        /><label for="all">全て</label>
        <input
          type="radio"
          id="now"
          value="作業中"
          v-model="radioValue"
          @change="showStatus"
        /><label for="now">作業中</label>
        <input
          type="radio"
          id="finish"
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
        <tbody id="todo-lists-wrap" >
          <tr v-for="(todo, index) in todos" :key="todo.comment">
            <td class="id">{{ index }}</td>
            <td>{{ todo.comment }}</td>
            <td class="status-value" @click="changeStatus()">{{ status }}</td>
            <td @click="deleteComment(index)">{{ deleteBtn }}</td>
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
      status: '作業中',
      deleteBtn: '削除',
      radioValue: '全て',
    };
  },
  methods: {
    addComment() {
      const todo = {};
      todo.comment = this.value;
      this.todos.push(todo);
      this.value = '';
      setTimeout(function(){
        this.showStatus();
        console.log(this)
      }.bind(this), 0);
    },
    changeStatus() {
      if (event.target.textContent === '作業中') {
        event.target.textContent = '完了';
      } else {
        event.target.textContent = '作業中';
      }
    },
    deleteComment(id) {
      this.todos.splice(id, 1);
    },
    showStatus() {
      const statusValue = document.getElementsByClassName('status-value');
      for (let i = 0; i < statusValue.length; i++) {
        const statusItem = statusValue[i];
        console.log(statusItem.textContent);
        statusItem.parentNode.style.display = '';
        if (this.radioValue === '全て') {
          statusItem.parentNode.style.display = '';
        } else if (
          this.radioValue === '作業中' &&
          statusItem.textContent === '完了'
        ) {
          statusItem.parentNode.style.display = 'none';
        } else if (
          this.radioValue === '完了' &&
          statusItem.textContent === '作業中'
        ) {
          statusItem.parentNode.style.display = 'none';
        }
      }
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
