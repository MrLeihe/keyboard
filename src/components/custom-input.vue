<template>
  <div class="custom-input" @click="handleClick">
    <span class="input-value">{{ inputData.value }}</span>
    <span class="cursor" v-show="inputData.isFocus"></span>
    <span class="placeholder" v-show="!inputData.value">{{ inputData.placeholder }}</span>
  </div>
</template>

<script>
export default {
  name: 'CustomInput',
  props: {
    inputData: {
      type: Object,
      default: () => {
        return {
          name: '',
          value: '',
          placeholder: '',
          isFocus: false,
        }
      },
    },
  },
  methods: {
    handleClick() {
      this.$emit('click', this.inputData.name)
    },
  },
}
</script>

<style>
.custom-input {
  width: 80%;
  height: 30px;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 2px 10px;
  font-size: 16px;
  position: relative;
  left: 0;
  text-align: left;
  display: flex;
  align-items: center;
}

.placeholder {
  position: absolute;
  left: 11px;
  top: 50%;
  transform: translateY(-50%);
  color: #999;
}

.cursor {
  width: 2px;
  height: 18px;
  margin-top: -2px;
  margin-left: 1px;
  border-radius: 1px;
  background-color: #666;
  animation: blink 3s infinite;
}

@keyframes blink {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}
</style>
