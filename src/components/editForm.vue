<template>
  <div class="dialog">
    <div class="data-form">
      <div>
        Number:
        <input
          type="number"
          :min="min"
          :max="max"
          :disabled="Boolean(editData)"
          v-model="number"
        >
      </div>
      <div>
        Password:
        <input
            type="text"
            :disabled="true"
            v-model="password"
        >
      </div>
      <div>
        <input type="button" value="generate" @click="generate">
      </div>
      <div>
        <input type="button" :value="successBtnName" @click="success">
        <input type="button" value="cancel" @click="cancel">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "editForm",
  props: {
    nodeId: { required: false, type: [Number, Boolean], default: false },
    editData: { required: false, type: [Object, Boolean], default: false },
  },
  mounted() {
    if (this.editData) {
      this.id = this.editData.id
      this.name = this.editData.name
      this.password = this.editData.password
      this.number = this.editData.number
    } else {
      this.getRange()
    }
  },
  computed: {
    successBtnName() {
      return this.editData ? 'save' : 'add'
    }
  },
  data() {
    return {
      min: 1,
      max: 999,

      id: null,
      name: null,
      password: '',
      number: 1
    }
  },
  methods: {
    getRange() {
      // запрашиваем диапазон в api
      // fakeData
      let range = {
        min: 10,
        max: 20
      }
      // записываем после получения
      this.min = range.min
      this.max = range.max
      this.number = range.min
    },
    success() {
      if (this.editData) {
        // отправляем запрос на изменение данных
        console.log({
          id: this.id,
          password: this.password
        })
      } else {
        console.log({
          number: this.number,
          password: this.password
        })
        // отправляем запрос на добавление данных
      }
      // при успешном добавении/сохраенении
      this.$emit('action-completed')
      // в случае ошибки выводим ошибку, форму оставляем открытой
    },
    cancel() {
      this.$emit('close')
    },
    generate() {
      // отправяем запрос для генерации
      // устанавливаем полученное значение
      this.password = Math.round(Math.random() * 10000000).toString()
    }
  }
}
</script>

<style scoped>
.dialog {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #000000a1;
  z-index: 998;

  display: flex;
  align-items: center;
  justify-content: center;
}
.data-form {
  display: flex;
  flex-direction: column;
  background-color: #fff;
  padding: 10px;
}
.data-form>div {
  display: flex;
  justify-content: space-between;
  margin: 5px;
}
.data-form>div>input:not([type=button]) {
  width: 80px;
  margin-left: 20px;
}
</style>