<template>
  <div class="home">
    <h1>Index Page</h1>
    <h2>테스트 요청을 보내봅시다.</h2>
    <div>
      <button @click="onClickTestBtn">테스트 요청</button>
      <button @click="onClickCreateUserBtn">테스트 유저 생성</button>
      <button @click="onClickTestRequestBtn">테스트 요청 전송</button>
      {{ data }}
    </div>
  </div>
</template>
<script setup lang="ts">
import axios from "axios";
import type { AxiosResponse } from "axios";

definePageMeta({
  layout: "default",
});

interface UserRequest {
  name: string;
  job: string;
}

interface UserResponse {
  name: string;
  job: string;
  id: string;
  createdAt: string;
}

const data = ref<string | UserResponse>("");

async function onClickTestBtn() {
  const res = await axios.get("https://reqres.in/api/users?page=2");
  data.value = res.data;
}

async function onClickCreateUserBtn() {
  const res = await axios.post<UserRequest, AxiosResponse<UserResponse>>(
    "https://reqres.in/api/users",
    {
      name: "foo",
      job: "bar",
    }
  );
  data.value = res.data;
}

async function onClickTestRequestBtn() {
  try {
    const res = await axios.get(
      "https://eaed5e51-7e78-4177-ba49-66e094bba04c.mock.pstmn.io/TEST"
    );
    alert(`요청 성공!: ${res}`);
  } catch (e) {
    console.log(e);
  }
}
</script>
<style lang="scss" scoped></style>
