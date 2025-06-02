<template>
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <NuxtImg src="/assets/cart.jpg" class="mx-auto h-20 w-auto" />
      <h2
        class="mt-10 text-center text-2xl/9 font-bold tracking-tight text-gray-900"
      >
        Tambah Produk
      </h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <Form
        @submit="onSubmit"
        :validation-schema="schema"
        class="space-y-6"
        enctype="multipart/form-data"
      >
        <div>
          <label
            for="nama_product"
            class="block text-sm/6 font-medium text-gray-900"
            >Nama Produk</label
          >
          <div class="mt-2">
            <Field
              name="nama_product"
              id="nama_product"
              type="text"
              class="border block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6"
            />
            <ErrorMessage class="text-red-500" name="nama_product" />
          </div>
        </div>

        <div>
          <label
            for="deskripsi"
            class="block text-sm/6 font-medium text-gray-900"
            >Deskripsi</label
          >
          <div class="mt-2">
            <Field
              as="textarea"
              name="deskripsi"
              id="deskripsi"
              class="border block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6"
            />
            <ErrorMessage class="text-red-500" name="deskripsi" />
          </div>
        </div>

        <div>
          <label for="gambar" class="block text-sm/6 font-medium text-gray-900"
            >Gambar</label
          >
          <div class="mt-2">
            <input
              type="file"
              id="gambar"
              name="gambar"
              @change="handleFileChange"
              class="block w-full text-sm text-gray-900 border border-gray-300 rounded-md cursor-pointer bg-white focus:outline-none"
            />
            <span v-if="fileName" class="text-sm text-gray-500 mt-1">{{
              fileName
            }}</span>
          </div>
        </div>

        <div>
          <button
            type="submit"
            class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            Simpan
          </button>
        </div>
      </Form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";
import { useRouter } from "vue-router";

const schema = yup.object({
  nama_product: yup.string().required("Nama produk harus diisi"),
  deskripsi: yup.string().required("Deskripsi harus diisi"),
});

const router = useRouter();
let selectedFile: File | null = null;
const fileName = ref("");

const handleFileChange = (event: Event) => {
  const target = event.target as HTMLInputElement;
  if (target.files && target.files.length > 0) {
    selectedFile = target.files[0] || null;
    fileName.value = selectedFile ? selectedFile.name : "";
  }
};

const onSubmit = async (values: any) => {
  const formData = new FormData();
  formData.append("nama_product", values.nama_product);
  formData.append("deskripsi", values.deskripsi);
  if (selectedFile) {
    formData.append("gambar", selectedFile);
  }

  try {
    await $fetch("http://localhost:8080/api/products", {
      method: "POST",
      body: formData,
      credentials: "include",
    });
    router.push("/product");
  } catch (error) {
    console.error("Gagal menambahkan produk:", error);
  }
};
</script>

<style scoped></style>
