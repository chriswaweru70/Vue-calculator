<template>
  <div class="calculator">
    <div class="display"> {{ current || '0' }}</div>
    <div @click="clear" class="btn1">AC</div>
    <div @click="sign" class="btn1">+/-</div>
    <div @click="percent" class="btn1">%</div>
    <div @click="divide" class="operator">÷</div>
    <div @click="append('7')" class="btn1">7</div>
    <div @click="append('8')" class="btn1">8</div>
    <div @click="append('9')" class="btn1">9</div>
    <div @click="times" class="operator">x</div>
    <div @click="append('4')" class="btn1">4</div>
    <div @click="append('5')" class="btn1">5</div>
    <div @click="append('6')" class="btn1">6</div>
    <div @click="minus" class="operator">-</div>
    <div @click="append('1')" class="btn1">1</div>
    <div @click="append('2')" class="btn1">2</div>
    <div @click="append('3')" class="btn1">3</div>
    <div @click="add" class="operator">+</div>
    <div @click="append('0')" class=" btn1 zero">0</div>
    <div @click="dot" class="btn1">.</div>
    <div @click="equal" class="operator">=</div>
    
    </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
      }
  },
  methods: {
      clear() {
          this.current = '';
      },
      sign() {
         this.current = this.current.charAt(0) === '-' ? 
         this.current.slice(1) : `-${this.current}`;
      },
      percent () {
        this.current = `${parseFloat(this.current) / 100}`
      },
      append (number) {
        if (this.operatorClicked) {
           this.current= '';
           this.operatorClicked = false;
        }
          this.current =  `${this.current}${number}`;
      },
      dot () {
        if (this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },
      divide () {
        this.operator = (a, b) => a/b;
        this.previous = this.current;
        this.operatorClicked = true;      
      },
      times () {
        this.operator = (a, b) => a*b;
        this.previous = this.current;
        this.operatorClicked = true;
      },
      minus () {
        this.operator = (a, b) => a-b;
        this.previous = this.current;
        this.operatorClicked = true;
      },
      add () {
        this.operator = (a, b) => a+b;
        this.previous = this.current;
        this.operatorClicked = true;
      },
      equal () {
        this.current = `${this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
          )}`;
          this.previous = null;
      }
  }
}  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../views/styles.css'

</style>
