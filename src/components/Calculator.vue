<template>
 <section class="root">
   <div class="calculator">
     <div class="display">{{ display }}</div>
     <div class="keyboard">
       <div class="numbers">
          <button v-for="(number, i) in numbers" :key="i" class="number-btn" @click='handleNumber(number)'> {{ number }} </button>
       </div>
       <div class="basicOperations">
        <button class="operation-btn" 
          @click='division()'>/</button>
        <button class="operation-btn" 
          @click='multiplication()'>X</button>
        <button class="operation-btn" 
          @click='subtraction()'>-</button>
        <button class="operation-btn" 
          @click='sum()'>+</button>

        <button class="operation-btn"
          @click='result()'>=</button>
       </div>
       <div class="controllers">
          <button class="controller-btn clean" 
            @click='clean()'>C</button>
          <button class="controller-btn module"
            @click='signal()'>+/-</button>
          <button class="controller-btn percent"
            @click="percent()">%</button>
       </div>
     </div>
   </div>
 </section>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      numbers: ['7', '8', '9', '4', '5', '6', '1', '2', '3', '0', '.'],
      number: '',
      oldNumber: '',
      operation: null,
      opChoosed: false
    }
  },
  computed: {
    display () {
      return this.number
    }
  },
  methods: {
    handleNumber (value) {
      if (this.opChoosed) {
        this.number = ''
        this.opChoosed = false
      }

      this.number = `${this.number}${value}`
    },
    setValue() {
      this.oldNumber = this.number
      this.opChoosed = true
    },
    clean () {
      this.number = ''
      this.oldNumber = ''
    },
    signal () {
      this.number = this.number.charAt(0) === '-'
        ? this.number.slice(1)
        : `-${this.number}`
    },
    percent () {
      this.number = `${parseFloat(this.number) / 100}`
    },
    result () {
      this.number = `${this.operation(
        parseFloat(this.oldNumber),
        parseFloat(this.number)
      )}`
      this.oldNumber = ''
    },
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