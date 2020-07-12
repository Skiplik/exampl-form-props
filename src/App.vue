<template>
  <div id="app">
    <div>
      <input type="button" value="add" @click="clickAdd">
    </div>
    <div>
      <table class="table">
        <tr>
          <th>Number</th>
          <th>Name</th>
          <th>Password</th>
          <th>Actions</th>
        </tr>
        <tr
            v-for="(data,index) in list"
            :key="`td-${index}`"
        >
          <td>{{ data.number }}</td>
          <td>{{ data.name }}</td>
          <td>{{ data.password }}</td>
          <td>
            <input type="button" value="edit" @click="clickEdit(data)">
          </td>
        </tr>
      </table>
    </div>
    <edit-form
        v-if="showForm"
        :nodeId="selectedTreeNode.id"
        :editData="editData||false"
        @action-completed="refreshTable"
        @close="closeForm"
    />
  </div>
</template>

<script>
import editForm from './components/editForm'
export default {
  name: 'App',
  components: {
    editForm
  },
  data() {
    return {
      selectedTreeNode: {
        id: 1,
        otherProperties: '...'
      },
      // fakedata - получаем из запроса
      list: [
        { number: 0, name: 'Name 0', password: '0000000', id: '000' },
        { number: 1, name: 'Name 1', password: '0000001', id: '0001' },
        { number: 2, name: 'Name 2', password: '0000002', id: '002' },
        { number: 3, name: 'Name 3', password: '0000003', id: '003' },
        { number: 4, name: 'Name 4', password: '0000004', id: '004' },
        { number: 5, name: 'Name 5', password: '0000005', id: '005' },
        { number: 6, name: 'Name 6', password: '0000006', id: '006' },
        { number: 7, name: 'Name 7', password: '0000007', id: '007' },
        { number: 8, name: 'Name 8', password: '0000008', id: '008' },
        { number: 9, name: 'Name 9', password: '0000009', id: '009' }
      ],
      editData: null,
      showForm: false
    }
  },
  methods: {
    clickAdd() {
      this.editData = false
      this.showForm = true
    },
    clickEdit(data) {
      this.editData = data
      this.showForm = true
    },
    closeForm() {
      this.showForm = false
      this.editData = false
    },
    refreshTable() {
      this.closeForm()
      console.log('Добавление/Редактирование выполнено. Обновляем данные таблицы')
    }
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  padding: 10px;
}
input[type=button] {
  cursor: pointer;
}
.table {
  width: 100%;
  min-width: 500px;
  margin-top: 1rem;
  border-collapse: collapse;
}

.table th, .table td {
  border: 1px solid #000;
  text-align: center;
}
</style>
