<template>
  <div>
    <div class="btn-group">
      <button class="button" default>Alphabetic</button>
      <button class="button">Categorized</button>
    </div>
    <table class="table">
      <tr>
        <td>(Name)</td>
        <td>
          <input
            type="text"
            :value="getSelectedControl.name"
            @input="handleChangeInput($event,'name')"
          />
        </td>
      </tr>
      <tr>
        <td>BackColor</td>
        <td>
          <select
            :value="getSelectedControl.style.backgroundColor"
            @change="changeInput($event,'backgroundColor')"
          >
            <option v-for="(item,key) in backColor" :key="key" :value="item">{{key}}</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>ControlTipText</td>
        <td>
          <input
            type="text"
            :value="getSelectedControl.title"
            @input="handleChangeInput($event,'title')"
          />
        </td>
      </tr>
      <tr>
        <td>Enabled</td>
        <td>
          <select
            v-model="getSelectedControl.enabled"
            @change="handleEnabled(getSelectedControl.enabled)"
          >
            <option selected :value="true">True</option>
            <option :value="false">False</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>Font</td>
        <td>
          <select :value="getSelectedControl.style.font" @change="changeInput($event,'font')">
            <option v-for="(value,key) in font" v-bind:value="value" :key="key">{{key}}</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>ForeColor</td>
        <td>
          <select :value="getSelectedControl.style.color" @change="changeInput($event,'color')">
            <option v-for="(value,key) in foreColor" v-bind:value="value" :key="key">{{key}}</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>Height</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.style.height  | sizeFilter"
            @change="handleSizeForControls($event,getSelectedControl,'height')"
            @keyup.enter="handleSizeForControls($event,getSelectedControl,'height')"
          />
        </td>
      </tr>
      <tr>
        <td>HelpContextId</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.helpContextId"
            @input="handleChangeInput($event,'helpContextId')"
          />
        </td>
      </tr>
      <tr>
        <td>Left</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.style.left  | sizeFilter"
            @change="handleSizeForControls($event,getSelectedControl,'left')"
            @keyup.enter="handleSizeForControls($event,getSelectedControl,'left')"
          />
        </td>
      </tr>
      <tr>
        <td>MouseIcon</td>
        <td>
          <input type="file" />
        </td>
      </tr>
      <tr>
        <td>MousePointer</td>
        <td>
          <select :value="getSelectedControl.style.cursor" @change="changeInput($event,'cursor')">
            <option v-for="(value,key) in mousePointer" v-bind:value="value" :key="key">{{key}}</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>MultiRow</td>
        <td>
          <select
            v-model="getSelectedControl.multiRow"
            @change="handleChangeInput($event,'multiRow')"
          >
            <option :value="true">True</option>
            <option :value="false">False</option>
          </select>
        </td>
      </tr>
       <tr>
        <td>Style</td>
        <td>
          <select :value="getSelectedControl.style1" @change="handleChangeInput($event,'style1')">
            <option v-for="(value,key) in style" v-bind:value="value" :key="key">{{key}}</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>TabFixedHeight</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.tabFixedHeight | sizeFilter"
            @change="handleChangeInputNumber($event,'tabFixedHeight')"
          />
        </td>
        <tr>
        <td>TabFixedWidth</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.tabFixedWidth | sizeFilter"
             @change="handleChangeInputNumber($event,'tabFixedWidth')"
          />
        </td>
        </tr>
      
      <tr>
        <td>TabIndex</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.tabindex"
            @input="handleChangeInput($event,'tabindex')"
          />
        </td>
      </tr>
      <tr>
        <td>TabOrientation</td>
        <td>
          <select :value="getSelectedControl.tabOrientation" @change="handleChangeInput($event,'tabOrientation')">
            <option v-for="(value,key) in tabOrientation" v-bind:value="value" :key="key">{{key}}</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>TabStop</td>
        <td>
          <select :value="getSelectedControl.tabStop" @change="handleChangeInput($event,'tabStop')">
            <option :value="false" selected>False</option>
            <option :value="true">True</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>Tag</td>
        <td>
          <input
            type="text"
            :value="getSelectedControl.tag"
            @input="handleChangeInput($event,'tag')"
          />
        </td>
      </tr>
      <tr>
        <td>Top</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.style.top  | sizeFilter"
            @change="handleSizeForControls($event,getSelectedControl,'top')"
            @keyup.enter="handleSizeForControls($event,getSelectedControl,'top')"
          />
        </td>
      </tr>
      <tr>
        <td>Value</td>
        <td>
          <input
            type="number"
            v-model="getSelectedControl.value"
             @change="handleChangeInputNumber($event,'value')"
          >
        </td>
      </tr>
      <tr>
        <td>Visible</td>
        <td>
          <select :value="getSelectedControl.visible" @change="handleChangeInput($event,'visible')">
            <option :value="false">False</option>
            <option :value="true" selected>True</option>
          </select>
        </td>
      </tr>
      <tr>
        <td>Width</td>
        <td>
          <input
            type="number"
            :value="getSelectedControl.style.width  | sizeFilter"
            @change="handleSizeForControls($event,getSelectedControl,'width')"
            @keyup.enter="handleSizeForControls($event,getSelectedControl,'width')"
          />
        </td>
      </tr>
    </table>
  </div>
</template>

<script lang="ts">
/* eslint-disable */

import { Component, Prop, Vue } from "vue-property-decorator";
import backColor from "../models/backColor.json";
import backStyle from "../models/backStyle.json";
import borderColor from "../models/borderColor.json";
import borderStyle from "../models/borderStyle.json";
import font from "../models/font.json";
import foreColor from "../models/foreColor.json";
import mousePointer from "../models/mousePointer.json";
import picturePosition from "../models/picturePosition.json";
import specialEffect from "../models/specialEffect.json";
import textAlign from "../models/textAlign.json";
import orientation from "../models/orientation.json"
import { validators } from "../validators/validator";
import { Mutation, Getter, Action } from "vuex-class";
import { EventBus } from "./event-bus";
import { OVERFLOW, INVALID_VALUE, INVALID_PICTURE } from "../utils/constant";
import style from "../models/style.json"
import tabOrientation from "../models/tabOrientation.json"

@Component({
  filters: {
    sizeFilter(value: any) {
      return parseInt(value, 10);
    }
  }
})
export default class TabStripTable extends Vue {
  @Prop() selectedUserForm: any;
  validators: object = validators;
  backColor: object = backColor;
  borderColor: object = borderColor;
  borderStyle: object = borderStyle;
  backStyle: object = backStyle;
  font: object = font;
  foreColor: object = foreColor;
  mousePointer: object = mousePointer;
  specialEffect: object = specialEffect;
  picturePosition: object = picturePosition;
  textAlign: object = textAlign;
  orientation: object = orientation;
  style: object = style;
  tabOrientation: object = tabOrientation;

  @Getter getSelectedControl!: any;
  @Mutation updateControl!: any;
  @Mutation updateControlStyle!: any;
  //
  @Action updatePicturePositionAction!: any;
  @Action updateAcceleratorAction!: any;
  @Action updateCaption!: any;

  @Mutation updatecaptionAutoSize!: any;


  handleAlignment(e:any,styleName:any){
    debugger
    let value = e.target.value
      console.log(e.target.value)
      if(value==="1 - fmAlignmentRight"){
          this.updateControl({ styleValue: e.target.value, styleName: styleName})
      } else{
          this.updateControl({ styleValue: e.target.value, styleName: styleName})
      }
  }

  

  ////////////validation
  handleSizeForControls(event: any, getSelectedControl: any, styleName: any) {
    debugger;
    const result = validators.sizeValidateForControls(
      event,
      getSelectedControl,
      styleName
    );
    if (event.target.value.length <= 12) {
      if (result === false) {
        debugger;
        EventBus.$emit("Popup", OVERFLOW, true);
      }
    } else {
      EventBus.$emit("Popup", INVALID_VALUE, true);
    }
  }

  handlePicture(event: any, getSelectedControl: any, styleName: any) {
    debugger;
    const result = validators.imageValidateForControls(
      event,
      getSelectedControl,
      styleName
    );
    if (!event.target.files[0].name.match(/.(jpg|jpeg|png|gif)$/i)) {
      debugger;
      EventBus.$emit("Popup", INVALID_PICTURE);
    } else {
    }
  }

  mounted() {
    console.log("Asd", this.getSelectedControl);
  }



  handleChangeInput(e: any, styleName: string) {
    // debugger;
    console.log("inputd", e.target.value);
    this.updateControl({ styleValue: e.target.value, styleName: styleName });
  }
  handleChangeInputNumber(e: any, styleName: string) {
    // debugger;
    console.log("inputd", e.target.value);
    this.updateControl({ styleValue: parseInt(e.target.value), styleName: styleName });
  }

  changeInput(e: any, styleName: string) {
    this.updateControlStyle({
      styleValue: e.target.value,
      styleName: styleName
    });
  }



  ////////////////////

  autoSizeChange(e: any, styleName: string) {
    debugger;
    if (e.target.value === "true") {
      this.updateControl({ styleValue: e.target.value, styleName: styleName });
      EventBus.$emit("autoSize", this.getSelectedControl.style);
    } else {
      this.updateControl({ styleValue: e.target.value, styleName: styleName });
    }
  }
  handleEnabled(data: boolean) {
    if (data) {
      this.getSelectedControl.style.color = "black";
    } else {
      this.getSelectedControl.style.color = "#DCDCDC";
    }
  }
  wordWrapChange(event: any) {
    debugger;
    if (event.target.value === "true") {
      this.getSelectedControl.style.wordWrap = "break-word";
      this.getSelectedControl.style.whiteSpace = "normal";
    } else {
      this.getSelectedControl.style.wordWrap = "normal";
      this.getSelectedControl.style.whiteSpace = "nowrap";
    }
  }

  handleCaption(e: any, styleName: string) {
    debugger;
    let that = this;
    this.updateCaption({
      styleValue: e.target.value,
      styleName: styleName
    }).then(() => {
      if (this.getSelectedControl.autoSize === "true") {
        debugger;
        EventBus.$emit("autoSize", that.getSelectedControl.style);
      }
    });
  }

  handleAccelerator(event: any, styleName: string) {
    this.updateAcceleratorAction({
      styleValue: event.target.value[0],
      styleName: styleName
    });
  }

  handlePicturePosition(
    event: any,
    PropName: string,
    styleName1: string,
    styleName2: string
  ) {
    this.updatePicturePositionAction({
      sName1: styleName1,
      sName2: styleName2,
      styleValue: event.target.value
    });
  }
}
</script>

<style scoped>
.node {
  text-align: left;
}
table,
th,
td {
  /* table-layout: fixed; */
  margin-right: 0%;
  width: 100%;
  border: 1px solid black;
  border-collapse: collapse;
  color: black;
}
th,
td {
  text-align: left;
  font-size: 11px;
}
th {
  width: 120%;
  font-size: 12px;
}
.form-control {
  float: left;
  width: 280px;
  cursor: pointer;
  background-color: rgb(190, 185, 185);
  /* border: 6px solid grey; */
}
label {
  float: left;
}
select {
  /* width: 100%; */
  width: 166px;
  padding: 1px 2px;
}

/* Must be added as style for the new data */
.btn-group .button {
  border: none;
  color: black;

  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
  cursor: pointer;
  /* float: left; */
}
.btn-group .button {
  border: none;
  color: black;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 12px;
  cursor: pointer;
  /* float: left; */
}
</style>