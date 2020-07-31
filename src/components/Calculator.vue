<style src="./Calculator.css" scoped></style>

<template>
 <section class="root">
    <div class="calculator">
      <div class="display">{{ display }}</div>
      <button @click='clean()'>C</button>
      <button @click='signal()'>+/-</button>
      <button @click="percent()">%</button>  
      <button @click='division()'>/</button>
      <button @click='handleNumber("7")'>7</button>
      <button @click='handleNumber("8")'>8</button>
      <button @click='handleNumber("9")'>9</button>
      <button class="operation" @click='multiplication()'>X</button>
      <button @click='handleNumber("4")'>4</button>
      <button @click='handleNumber("5")'>5</button>
      <button @click='handleNumber("6")'>6</button>
      <button class="operation" @click='subtraction()'>-</button>
      <button @click='handleNumber("1")'>1</button>
      <button @click='handleNumber("2")'>2</button>
      <button @click='handleNumber("3")'>3</button>
      <button class="operation" @click='sum()'>+</button>
      <button class="zero-btn" @click='handleNumber("0")'>0</button>
      <button @click='handleNumber(".")'>.</button>
      <button class="operation" @click='result()'>=</button>
    </div>
 </section>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      number: '',
      oldNumber: '',
      operation: null,
      opChoosed: false
    }
  },
  computed: {
    display () {
      return this.number || '0'
    }
  },
  methods: {

    // here I join the actual number with the next one clicked

    handleNumber (value) {
      if (this.opChoosed) {
        this.number = ''
        this.opChoosed = false
      }

      this.number = `${this.number}${value}`
    },

    // here I set the new calculated value to Old number, so the user can continue calculating
    setValue() {
      this.oldNumber = this.number
      this.opChoosed = true
    },


    // options

    clean () {
      this.number = ''
      this.oldNumber = ''
    },
    signal () {
      if (this.number) {
        this.number = this.number.charAt(0) === '-'
          ? this.number.slice(1)
          : `-${this.number}`
      }
    },
    percent () {
      if (this.number) {
      this.number = `${parseFloat(this.number) / 100}`
      }
    },
    result () {
      if (this.number && this.oldNumber) {
          this.number = `${this.operation(
          parseFloat(this.oldNumber),
          parseFloat(this.number)
        )}`
        this.oldNumber = ''
      }
    },


    // basic operations 
    // notice that I return an arrow function to our operation, then I can use it on result func

    division () {
      this.operation = (num1, num2) => num1 / num2
      this.setValue()
    },
    multiplication () {
      this.operation = (num1, num2) => num1 * num2
      this.setValue()
    },
    subtraction () {
      this.operation = (num1, num2) => num1 - num2
      this.setValue()
    },
    sum () {
      this.operation = (num1, num2) => num1 + num2
      this.setValue()
    }
  }
}
</script>