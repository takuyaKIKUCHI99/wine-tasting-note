<template>
  <div>
    <el-form-item label="外観" />
    <el-form-item :label="`清澄度(${appearanceForm.clarity.length}/1)`">
      <el-checkbox-group v-model="appearanceForm.clarity">
        <el-checkbox
          v-for="(option, index) in appearanceOptions.clarityOptions"
          :key="index"
          :label="option"
          :value="option"
        ></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item :label="`輝き(${appearanceForm.brightness.length}/1)`">
      <el-checkbox-group v-model="appearanceForm.brightness">
        <el-checkbox
          v-for="(option, index) in appearanceOptions.brightnessOptions"
          :key="index"
          :label="option"
          :value="option"
        ></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item :label="`色調(${appearanceForm.tone.length}/2)`">
      <el-checkbox-group v-model="appearanceForm.tone">
        <el-checkbox
          v-for="(option, index) in appearanceOptions.toneOptions"
          :key="index"
          :label="option"
          :value="option"
        ></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item :label="`濃淡(${appearanceForm.shades.length}/1)`">
      <el-checkbox-group v-model="appearanceForm.shades">
        <el-checkbox
          v-for="(option, index) in appearanceOptions.shadesOptions"
          :key="index"
          :label="option"
          :value="option"
        ></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item :label="`粘性(${appearanceForm.viscosity.length}/1)`">
      <el-checkbox-group v-model="appearanceForm.viscosity">
        <el-checkbox
          v-for="(option, index) in appearanceOptions.viscosityOptions"
          :key="index"
          :label="option"
          :value="option"
        ></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item
      :label="`外観の印象(${appearanceForm.appearanceImpression.length}/2)`"
    >
      <el-checkbox-group v-model="appearanceForm.appearanceImpression">
        <el-checkbox
          v-for="(option,
          index) in appearanceOptions.appearanceImpressionOptions"
          :key="index"
          :label="option"
          :value="option"
        ></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from "vue-property-decorator";
import { FormItem, Checkbox, CheckboxGroup } from "element-ui";

import { AppearanceFields } from "@/types/types";

import { appearanceOptions } from "@/constants/appearanceOptions";

@Component({
  components: {
    "el-checkbox": Checkbox,
    "el-checkbox-group": CheckboxGroup,
    "el-form-item": FormItem
  }
})
export default class Appearance extends Vue {
  @Prop({ default: "red" }) wineType!: string;

  private appearanceForm: AppearanceFields = {
    clarity: [],
    brightness: [],
    tone: [],
    shades: [],
    viscosity: [],
    appearanceImpression: []
  };

  // Options
  private appearanceOptions = appearanceOptions(this.wineType);

  @Watch("wineType")
  updateOptions() {
    this.appearanceOptions = appearanceOptions(this.wineType);
  }

  @Watch("appearanceForm", { deep: true })
  updateForm() {
    this.$emit("updateForm", this.appearanceForm, "appearance");
  }
}
</script>
