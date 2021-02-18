<template>
  <div class="container">
    <GlobalHeader :user="user" />
    <!-- <ColumnList :list="testData" /> -->
    <validate-form @formSubmit="onFormSubmit">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <validate-input
          :rules="rules"
          v-model="emailValue"
          placeholder="请输入邮件地址"
          type="text"
        ></validate-input>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">密码</label>
        <validate-input
          :rules="rules1"
          v-model="passwordValue"
          placeholder="请输入密码"
          type="password"
        ></validate-input>
      </div>
      <!-- <button type="submit" class="btn btn-primary">Submit</button> -->
      <template #submit>
        <span class="btn btn-danger">submit</span>
      </template>
    </validate-form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import "bootstrap/dist/css/bootstrap.min.css";
// import HelloWorld from './components/HelloWorld.vue'
import ColumnList, { ColumnProps } from "./components/ColumnList.vue";
import GlobalHeader, { UserProps } from "./components/GlobalHeader.vue";
import ValidateInput, { RulesProp } from "./components/ValidateInput.vue";
import ValidateForm from "./components/ValidateForm.vue";
const testData: ColumnProps[] = [
  {
    id: 1,
    title: "1111",
    discription: "222",
    avatar:
      "https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png",
  },
  {
    id: 1,
    title: "1111",
    discription: "222",
    avatar:
      "https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png",
  },
  {
    id: 1,
    title: "1111",
    discription: "222",
    // avatar: 'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png'
  },
  {
    id: 1,
    title: "1111",
    discription: "222",
    avatar:
      "https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png",
  },
];
const user: UserProps = {
  name: "斌斌",
  isLogin: true,
};

export default defineComponent({
  name: "App",
  components: {
    // ColumnList,
    GlobalHeader,
    ValidateInput,
    ValidateForm,
  },
  setup() {
    const rules: RulesProp = [
      { type: "required", message: "can not be empty" },
      { type: "email", message: "请输入正确的邮箱地址" },
    ];
    const rules1: RulesProp = [
      { type: "required", message: "can not be empty" },
      { type: "password", message: "密码长度太短" },
    ];
    const emailValue = ref("");
    const passwordValue = ref("");
    
    const onFormSubmit = (result: boolean) => {
      console.log(result);
    };
    return {
      testData,
      user,
      rules,
      rules1,
      emailValue,
      passwordValue,
      onFormSubmit
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
</style>
