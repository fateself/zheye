<template>
  <div class="validate-input-container pb-3">
    <input
      type="email"
      class="form-control"
      :class="{ 'is-invalid': emailRef.error }"
      :value="emailRef.val"
      @input="changeValue"
      @blur="validateEmail"
      v-bind="$attrs"
    />
    <div
      class="form-text"
      :class="{ 'invalid-feedback': emailRef.error }"
      v-if="emailRef.error"
    >
      {{ emailRef.message }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, reactive } from "vue";
interface RuleProp {
  type: "required" | "email";
  message: string;
}
export type RulesProp = RuleProp[];
const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;
export default defineComponent({
  inheritAttrs: false,
  props: {
    rules: Array as PropType<RulesProp>,
    modelValue: String,
  },
  setup(props, context) {
    const emailRef = reactive({
      val: props.modelValue || "",
      error: false,
      message: "",
    });
    const validateEmail = () => {
      if (props.rules) {
        const allpassed = props.rules.every((rule) => {
          let passed = true;
          emailRef.message = rule.message;
          switch (rule.type) {
            case "required":
              passed = emailRef.val.trim() !== "";
              break;
            case "email":
              passed = emailReg.test(emailRef.val);
              break;
            default:
              break;
          }
          return passed;
        });
        emailRef.error = !allpassed;
      }
    };
    //处理数据的双向绑定
    const changeValue = (e: KeyboardEvent) => {
      const value = (e.target as HTMLInputElement).value;
      emailRef.val = value;
      context.emit("update:modelValue", value);
    };
    return {
      emailRef,
      validateEmail,
      changeValue,
    };
  },
});
</script>

<style>
</style>