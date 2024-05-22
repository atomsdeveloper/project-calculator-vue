<template>
  <div class="calculator">
    <DisplayCustom :value="displayValue" />
    <ButtonCustom label="AC" triple @onClick="clearMemory" />
    <ButtonCustom label="/" oparation @onClick="setOperation"/>
    <ButtonCustom label="7" @onClick="addDigit"/>
    <ButtonCustom label="8" @onClick="addDigit"/>
    <ButtonCustom label="9" @onClick="addDigit"/>
    <ButtonCustom label="*" operation @onClick="setOperation" />
    <ButtonCustom label="4" @onClick="addDigit"/>
    <ButtonCustom label="5" @onClick="addDigit"/>
    <ButtonCustom label="6" @onClick="addDigit"/>
    <ButtonCustom label="-" operation @onClick="setOperation" />
    <ButtonCustom label="1" @onClick="addDigit"/>
    <ButtonCustom label="2" @onClick="addDigit"/>
    <ButtonCustom label="3" @onClick="addDigit"/>
    <ButtonCustom label="+" operation @onClick="setOperation" />
    <ButtonCustom label="0" double @onClick="addDigit" />
    <ButtonCustom label="." @onClick="addDigit"/>
    <ButtonCustom label="=" operation @onClick="setOperation" />
  </div>
</template>

<script>
import DisplayCustom from "../components/DisplayCustom.vue"
import ButtonCustom from "../components/ButtonCustom.vue"

export default {
    data: function () {
      return {
        displayValue: "0",
        clearDisplay: false,
        operation: null,
        values: [0, 0],
        current: 0
      }
    },
    components: { DisplayCustom, ButtonCustom },
    methods: {
      clearMemory: function () {
        Object.assign(this.$data, this.$options.data())
      },
      setOperation: function (operation) {
        if(this.current === 0) {
          this.operation = operation
          this.current = 1
          this.clearDisplay = true 
        } else {
          const equals = operation === "="
          const currentOperation = this.operation

          try {
            this.values[0] = eval(`${this.values[0]} ${currentOperation} ${this.values[1]}`);

            if(isNaN(this.values[0] || !isFinite(this.values[0]))) {
              this.clearMemory()
              return
            }
          } catch (e) {
            this.$emit('onError', e)
          }

          this.values[1] = 0

          this.displayValue = this.values[0]
          this.operation = equals ? null : this.operation
          this.current = equals ? 0 : 1
          this.clearDisplay != equals
        }
      },
      addDigit: function (d) {
        if(d === "." && this.displayValue.includes(".")) {
          return
        }

        const clearDisplay = this.displayValue === "0" || this.clearDisplay
        const currentValue = clearDisplay ? "" : this.displayValue
        const displayValue = currentValue + d

        this.displayValue = displayValue
        this.clearDisplay = false
        this.values[this.current] = displayValue
      } 
    }
}
</script>

<style>
.calculator {
    width: 235px;
    height: 320px;

    overflow: hidden;
    border-radius: 5px;

    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>