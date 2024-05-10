<template>
  <div>
    <h1>Version is : 1</h1>
    <p v-if="isLoading">Loading Details :</p>
    <div v-if="detail">
      <table style="border: 1px">
        <tr>
          <td>id</td>
          <td>Name</td>
          <td>avatar</td>
          <td>createdAt</td>
        </tr>
        <tr v-for="(item, i) in detail">
          <td>{{ item?.id }}</td>
          <td>{{ item?.name }}</td>
          <td>
            <img :src="item?.avatar" style="height: 10px; width: 10px" />
          </td>
          <td>{{ item?.createdAt }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
const detail = ref(null);
const isLoading = ref(true);

const fetchDetails = async () => {
  const response = await fetch(
    "https://663e27c1e1913c476796bd6f.mockapi.io/api/details"
  );
  const data = await response.text(); // Get the response body as text
  detail.value = JSON.parse(data);

  isLoading.value = false;
};
fetchDetails();
</script>
<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
