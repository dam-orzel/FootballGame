<template>
  <div>
    <Table v-if="dataTable" :theData="dataTable" :config="config" />
  </div>
</template>

<script>
import Table from "@/components/table";

export default {
  components: {
    Table
  },
  data: () => ({
    dataTable: [],
    config: [
      {
        img_key: "avatar",
        name: "",
        image: true
      },
      {
        key: "first_name",
        key_second: "last_name",
        name: "Full name"
      },
      {
        edit: "edit",
        delete: "delete",
        name: "Action"
      }
    ]
  }),
  head() {
    return {
      title: `User list`
    };
  },
  async mounted() {
    const userList = await this.$axios.$get("users");
    this.dataTable = userList.data;
  }
};
</script>

<style></style>
