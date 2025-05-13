<template>
  <!--
  This example requires updating your template:

  ```
  <html class="h-full bg-white">
  <body class="h-full">
  ```
-->
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <!-- <img class="mx-auto h-10 w-auto" src="./public/assets/logo.jpg" alt="Your Company"> -->
      <NuxtImg src="/assets/store-logo.png" class="mx-auto h-40 w-40" />

      <h2 class="mt-10 text-center text-2xl/9 font-bold tracking-tight text-gray-900">Register</h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <Form @submit="onSubmit" :validation-schema="schema" class="space-y-6" action="#" method="POST">
        <div>
          <label for="nama_lengkap" class="block text-sm/6 font-medium text-gray-900">Nama Lengkap</label>
          <div class="mt-2">
            <Field type="text" name="nama_lengkap" id="nama_lengkap" autocomplete="nama_lengkap" required
              class="border-2 block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" />
            <ErrorMessage class="text-red-500 text-xs font-medium" name="nama_lengkap" />
          </div>
        </div>

        <div>
          <label for="username" class="block text-sm/6 font-medium text-gray-900">Username</label>
          <div class="mt-2">
            <Field type="text" name="username" id="username" autocomplete="username" required
              class="border-2 block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" />
            <ErrorMessage class="text-red-500 text-xs font-medium" name="username" />
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label for="password" class="block text-sm/6 font-medium text-gray-900">Password</label>
          </div>
          <div class="mt-2">
            <Field type="password" name="password" id="password" autocomplete="current-password" required
              class="border-2 block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" />
            <ErrorMessage class="text-red-500 text-xs font-medium" name="password"/>
          </div>
        </div>

        <div class="flex flex-row justify-between ">
          <NuxtLink to="/" class=" ml-auto font-semibold text-indigo-600 hover:text-indigo-500">Silahkan masuk jika sudah memiliki akun
          </NuxtLink>
        </div>

        <div >
          <button type="submit"
            class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Register</button>
        </div>
      </Form>

      <p class="mt-10 text-center text-sm/6 text-gray-500">
        Not a member?
        <a href="#" class="font-semibold text-indigo-600 hover:text-indigo-500">Start a 14 day free trial</a>
      </p>
    </div>
  </div>
  <div>
    hello worlddd
  </div>
</template>

<script setup lang="ts">
import { Form, Field, ErrorMessage } from "vee-validate"
import * as yup from "yup"

const schema = yup.object({
  nama_lengkap: yup.string().required('Nama Lengkap harus diisi'),
  username: yup.string().required('Username harus diisi'),
  password: yup.string().required('Password harus diisi').min(5)
})
const onSubmit = async (values: any) => {
  const response = await $fetch('http://localhost:8080/register', {
    method: "POST",
    body: values,
    credentials: "include"
  })

  try{
    console.log(response)
  }catch (error) {
    console.log(error)
  }
}

</script>

<style scoped></style>