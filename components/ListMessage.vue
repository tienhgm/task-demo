<template>
  <table class="list-table">
    <thead>
      <tr>
        <th>#</th>
        <th style="width: 300px">List</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(e, index) in listInfo" :key="index">
        <td>{{ ++index }}</td>
        <td>
          <div class="name">
            {{ e.name }}
          </div>
          <div class="content">
            {{ e.content }}
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "list-message",
  props: {
    listInfo: { type: Array, default: null },
  },
};
</script>

<style scoped>
table tr {
  border-top: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
}
table {
  border-collapse: collapse;
}
th,
td {
  text-align: left;
  width: 120px;
}
table .name {
  font-size: 12px;
  color: #d798c1;
  font-weight: bold;
  line-height: 20px;
}
</style>