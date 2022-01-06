<template>
  <div class="custom-keyboard">
    <div class="title-wrap">
      <div class="label">苏打爱生活</div>
      <div class="complete" @click="hanleComplete">完成</div>
    </div>
    <ul @click="handleClick">
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>0</li>
      <li>Q</li>
      <li>W</li>
      <li>E</li>
      <li>R</li>
      <li>T</li>
      <li>Y</li>
      <li>U</li>
      <li>I</li>
      <li>O</li>
      <li>P</li>
      <li>A</li>
      <li>S</li>
      <li>D</li>
      <li>F</li>
      <li>G</li>
      <li>H</li>
      <li>J</li>
      <li>K</li>
      <li>L</li>
      <li class="cancel" @click="handleCancel">取消</li>
      <li>Z</li>
      <li>X</li>
      <li>C</li>
      <li>V</li>
      <li>B</li>
      <li>N</li>
      <li>M</li>
      <li class="delete" @click="handleDelete" @touchstart="onTouchstart" @touchend="onTouchend">删除</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Keyboard',
  methods: {
    handleClick(event) {
      if (event.target && !/li/i.test(event.target.nodeName)) {
        return
      }
      this.$emit('select', event.target.innerText)
    },
    hanleComplete() {
      this.$emit('complete')
    },
    handleCancel(event) {
      event.stopPropagation()
      this.$emit('cancel')
    },
    handleDelete(event) {
      event.stopPropagation()
      this.$emit('delete')
    },
    onTouchstart(event) {
      event.preventDefault()
      this.$emit('delete')
      this.timer = setInterval(() => {
        this.$emit('delete')
      }, 100)
    },
    onTouchend() {
      clearInterval(this.timer)
    },
  },
  beforeDestroy() {
    if (this.timer) {
      clearInterval(this.timer)
    }
  },
}
</script>

<style lang="less">
ul {
  padding: 0;
  text-align: left;
  margin: 0;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}

ul > li {
  list-style: none;
  width: 8.5%;
  height: 40px;
  line-height: 40px;
  text-align: center;
  margin: 0.75%;
  background: #fff;
  border-radius: 4px;
  font-size: 18px;
  font-weight: 500;
  display: inline-block;
  box-shadow: -1px 1px 1px #999;
}

.custom-keyboard {
  position: fixed;
  left: 0;
  bottom: 0;
  right: 0;
  background: #dbdbdb;
  padding-bottom: 5px;
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom);
}

.title-wrap {
  position: relative;
  height: 45px;
}

.label {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.complete {
  position: absolute;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  color: blue;
  padding: 10px;
}

.cancel {
  width: 12%;
  color: blue;
}

.delete {
  width: 14%;
  background: blue;
  color: #fff;
}
</style>
