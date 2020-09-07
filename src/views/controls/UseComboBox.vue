<template>
  <div
    class="custom-select"
    style="control.style"
    :style="{lineHeight:(control.columnCount!=1)?'50px':'15px'}"
    :tabindex="tabindex"
    @blur="open = false"
  >
    <!-- :style="{lineHeight:(optionHead[0]?'20px':((control.columnCount>=2)?'60px':'20px'))}" -->
    <div class="combobox">
      <input
        type="text"
        @focus="focus"
        @blur="blur"
        :style="{height:control.style.height}"
        :value="this.selected"
        ref="input"
      />
      <div
        class="selected"
        ref="selected"
        :style="{display:control.showDropButtonWhen==='block'?'block':expandWidth(),backgroundImage:control.dropButtonStyle==='0 - fmDropButtonStylePlain'?'none':changeDropButtonStyle(),backgroundPosition:control.dropButtonStyle==='1 - fmDropButtonStyleArrow'?'center':'bottom'}"
        :class="{open: open}"
        @click="open = !open"
      ></div>
      <div
        class="items"
        :style="{width:parseInt(control.listWidth)+'px',zIndex:999999999,left:(parseInt(control.listWidth)>1000)?(-(parseInt(control.listWidth)))%1000+'px':'0px'}"
        :class="{selectHide: !open}"
      >
        <!-- <span>{{control.columnHeads==='true'?makeTrue():makeTrue()}}</span> -->
        <span>{{control.columnCount!='1'?changeHeight():remainSame()}}</span>
        <div
          v-if="control.columnHeads === 'true'"
          class="columnHeads"
          :style="{gridTemplateColumns:(control.listStyle === '1 - fmListStyleOption')? '15px 100%': '0px 100%',borderRight: '0.1px solid black',borderLeft: '0.1px solid black'}"
        >
          <span
            v-if="control.listStyle === '1 - fmListStyleOption'"
            :style="{
              borderRight:
                control.listStyle === '1 - fmListStyleOption'
                  ? '0.1px solid black'
                  : '0px',
            }"
          ></span>
          <!-- <div style="padding-Left:5px">Column A</div> -->
        </div>
        <div
          class="item"
          v-for="(option, i) of optionHead"
          :key="i"
          @click="selected=option; open=false; $emit('input', option)"
        >
          <li>{{ option }}</li>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";
import { Mutation, Action, Getter } from "vuex-class";
import { EventBus } from "../../components/event-bus";
import "vue-select/dist/vue-select.css";
// import '../../assets/'

@Component({})
export default class UseComboBox extends Vue {
  @Prop() private control!: object;
  @Prop() private modal!: object;
  optionHead: any = [" "];
  options: any = [" "];

  @Prop() private tabindex = 0;

  open = false;

  selected = this.options.length > 0 ? this.options[0] : null;

  @Getter getPrevControlIndex!: any;
  @Mutation userFormIndex!: Function;
  @Mutation updatePrevControlIndex!: Function;
  @Mutation controlIndex!: Function;
  @Mutation updateControlIndex!: Function;
  @Mutation activateControl!: Function;

  customComoboBoxClick(e: any) {
    console.log("clickd");
    this.userFormIndex(this.modal);
    this.controlIndex(this.control);
    this.updatePrevControlIndex();
    this.updateControlIndex(this.getPrevControlIndex);
    this.activateControl();
    if (e.target.tagName === "INPUT") {
      (this as any).$refs.combobox.focus();
    } else if (e.target.tagName === "SELECT") {
      (this as any).$refs.selectcombo.focus();
    }
    EventBus.$emit("userFormClicked", this.control, this.modal);
  }

  mounted() {
    this.$emit("input", this.selected);
  }
  makeTrue() {
    if (this.control.columnHeads === "true") {
      this.optionHead = [" "];
      this.optionHead = [...this.options];
      this.optionHead.unshift(" ");
    } else if (this.control.columnHeads === "false") {
      this.optionHead = [" "];
      this.optionHead = [...this.options];
    }
  }
  changeHeight() {
    console.log("Height should change", this.control.columnCount);
    console.log(this.optionHead.length);
    this.optionHead[length];
  }
  remainSame() {
    console.log("Same", this.control.columnCount);
  }
  focus(e: any) {
    if (this.control.showDropButtonWhen === "focus") {
      (this as any).$refs.selected.style.display = "block";
      // console.log("Reference", (this as any).$refs.selected.style);
    }
  }
  blur(e: any) {
    if (this.control.showDropButtonWhen === "focus") {
      (this as any).$refs.selected.style.display = "none";
      (this as any).$refs.input.style.width = "calc(100% + 14px)";
      // (this as any).$refs.selected.style.width = "calc(100% + 20px)";
      // console.log('Reference',(this as any).$refs.selected.style)
    }
  }
  expandWidth() {
    if (this.control.showDropButtonWhen === "none") {
      debugger
      (this as any).$refs.selected.style.display = "none";
      (this as any).$refs.input.style.width = "calc(100% + 14px)";
      return 'none'
    }
  }
  changeDropButtonStyle() {
    if (this.control.dropButtonStyle === "1 - fmDropButtonStyleArrow") {
      return `url('https://img.icons8.com/android/24/000000/sort-down.png')`;
    } else if (
      this.control.dropButtonStyle === "2 - fmDropButtonStyleEllipsis"
    ) {
      return `url('https://img.icons8.com/ios-glyphs/30/000000/ellipsis.png')`;
    } else if (this.control.dropButtonStyle === "3 - fmDropButtonStyleReduce") {
      return `url('https://img.icons8.com/android/24/000000/minus.png')`;
    }
  }

  handleOptionInput(e: any, option: any) {
    e.target.checked = true;
  }

  handleMouseClick(e: any, option: any) {
    debugger;
    e.target.checked = true;
    this.selected = option;
    this.open = false;
    this.$emit("input", option);
  }

  handleMouseLeave(e: any) {
    e.target.checked = false;
  }
}
</script>



<style scoped>
.custom-select {
  position: relative;
  width: 300px;
  text-align: left;
  outline: none;
  /* height: 80px; */
  line-height: 15px;
  /* specify the drop down height */
  left: 20px;
  top: 15px;
  width: 80px;
  height: 100px;
  /* border: 1px solid red */
}
.columnHeads {
  height: 19.2px;
  border: 1px solid black;
  display: grid;
  grid-template-columns: 100%;
}
.selected {
  background-color: lightgray;
  /* border-radius: 6px; */
  border: 1px solid #858586;
  border-left: 0px;
  color: black;
  /* background-image: none; */

  background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="50" border="1px solid red"><polygon points="0,0 100,0 50,50" style="fill:%23666666;stroke-width:3;stroke:rgb(0,0,250)" /></svg>');
  background-size: 40%;
  background-position: center;
  background-repeat: no-repeat;
  cursor: pointer;
  /* user-select: none; */
  width: 20px;
  height: calc(100% - 2px);
}

.items {
  position: relative;
  color: black;
  background-color: white;
  overflow: hidden;
  left: 0;
  right: 0;
  width: calc(100% + 20px);
}

.item {
  /* list-style: none; */
  color: white;
  padding-left: 8px;
  cursor: pointer;
  border: 0.1px solid black;
}

.item:hover {
  background-color: white;
  /* color: white; */
  border: 0.1px solid black;
}

.selectHide {
  display: none;
}

.combobox {
  display: grid;
  grid-template-columns: 100% 20px;
}
.columnHeads {
  height: 19.2px;
  border: 1px solid black;
  border-top: 0px;
  display: grid;
  grid-template-columns: 20px 100%;
}
</style>