<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <CustomInput @click="handleShow" :inputData="inputFields.account" />
    <CustomInput @click="handleShow" :inputData="inputFields.password" />

    <Keyboard @select="handleSelect" @complete="handleComplete" @cancel="handleCancel" @delete="handleDelete" v-show="visible" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Keyboard from './components/keyboard.vue'
import CustomInput from './components/custom-input.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Keyboard,
    CustomInput,
  },
  data() {
    return {
      current: 'account',
      inputFields: {
        account: {
          name: 'account',
          value: '',
          placeholder: '请输入账号',
          isFocus: true,
        },
        password: {
          name: 'password',
          value: '',
          placeholder: '请输入密码',
          isFocus: false,
        },
      },
      visible: true,
    }
  },
  methods: {
    handleShow(name) {
      this.current = name
      Object.keys(this.inputFields).forEach(key => {
        this.inputFields[key].isFocus = key === name
      })
      this.visible = true
    },
    handleSelect(value) {
      const preValue = this.inputFields[this.current].value
      this.inputFields[this.current].value = preValue + value
    },
    handleComplete() {
      this.visible = false
    },
    handleCancel() {
      this.visible = false
    },
    handleDelete() {
      const curValue = this.inputFields[this.current].value
      if (this.value === '') {
        return
      }
      this.inputFields[this.current].value = curValue.slice(0, -1)
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  -webkit-user-select: none;
  user-select: none;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
</style>
