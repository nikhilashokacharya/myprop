<template>
  <div @click="customSpinButtonClick">
    <div>
      <div
        class="spin"
        :style="[control.style,{transform:control.orientation==='1 - fmOrientationHorizontal'?'rotate(90deg)':checkOtherOrientations()}]"
      >
        <button class="button-element-top" @click="increaseValue"></button>
        <button class="button-element-bottom" @click="decreaseValue"></button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";
import { Mutation, Action, Getter } from "vuex-class";
import { EventBus } from "../../components/event-bus";
@Component({
  components: {},
})
export default class UseSpinButton extends Vue {
  @Prop() private control!: object;
  @Prop() private modal!: object;
  @Getter getPrevControlIndex!: any;
  @Mutation userFormIndex!: Function;
  @Mutation updatePrevControlIndex!: Function;
  @Mutation controlIndex!: Function;
  @Mutation updateControlIndex!: Function;
  @Mutation activateControl!: Function;
  spinStyle = {
    width: "59px",
    height: "60px",
    transform: "rotate(0deg)",
  };
  spinStyle1 = {
    width: "61px",
    height: "60px",
    transform: "rotate(90deg)",
  };
  customSpinButtonClick() {
    this.userFormIndex(this.modal);
    this.controlIndex(this.control);
    this.updatePrevControlIndex();
    this.updateControlIndex(this.getPrevControlIndex);
    this.activateControl();
    // (this as any).$refs.refcheckbox.focus();
    EventBus.$emit("userFormClicked", this.control, this.modal);
    console.log("control", this.control);
  }
  checkOtherOrientations() {
    if (this.control.orientation === "1 - fmOrientaionVertical") {
      return "rotate(0deg)";
    } else if (this.control.orientation === "-1 - fmOrientationAuto") {
      if (this.control.style.height >= this.control.style.width) {
        return "rotate(0deg)";
      } else {
        return "rotate(90deg)";
      }
    }
  }
  increaseValue() {
    if (
      this.control.value <= this.control.max &&
      this.control.max - this.control.value > this.control.smallChange
    ) {
      this.control.value = this.control.value + this.control.smallChange;
    } else if (this.control.value <= this.control.max) {
      this.control.value = this.control.max;
    } else {
       this.control.value = this.control.max;
    }
  }
  decreaseValue() {
    if (
      this.control.value >= this.control.min &&
      this.control.value - this.control.min > this.control.smallChange
    ) {
      this.control.value = this.control.value - this.control.smallChange;
    } else if(this.control.value >= this.control.min){
      this.control.value = this.control.min;
    } else {
      this.control.value = this.control.min;
    }
    
  }
}
</script>

<style scoped>
.spin {
  display: grid;
  grid-template-columns: 1fr;
}
.button-element-top {
  background-image: url("../../assets/controls pictures/triangle-up-img.png");
  background-size: 40%;
  background-position: center;
  background-repeat: no-repeat;
  border-color: lightgrey;
}

.button-element-bottom {
  background-image: url("../../assets/controls pictures/triangle-down-img.png");
  background-size: 40%;
  background-position: center;
  background-repeat: no-repeat;
  border-color: lightgrey;
}
</style>