<template>
  <div class="custom-table">
    <table>
      <thead>
        <tr>
          <th v-for="(item, id) in config" :key="id">
            {{ item.name }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, id) in computedTableData" :key="id">
          <td v-for="(item, id) in config" :key="id">
            <img :src="row[item.img_key]" alt="" v-if="item.image" />
            <span>{{ row[item.key] }}</span>
            <span>{{ row[item.key_second] }}</span>
            <div class="table-action">
              <span v-if="item.edit">asd</span>
              <span v-if="item.delete">asd1</span>
            </div>
          </td>
        </tr>
      </tbody>
      <Pagination
        class="table-pagination"
        :totalRecords="theData.length"
        :perPageOptions="perPageOptions"
        v-model="pagination"
      />
    </table>
  </div>
</template>

<script>
import Pagination from "./pagination";

const perPageOptions = 3;

export default {
  components: {
    Pagination
  },
  data() {
    return {
      perPageOptions,
      pagination: { page: 1, perPage: perPageOptions }
    };
  },
  props: ["theData", "config"],
  computed: {
    computedTableData() {
      if (!this.searchTable) return [];
      else {
        const firstIndex = (this.pagination.page - 1) * this.pagination.perPage;
        const lastIndex = this.pagination.page * this.pagination.perPage;
        return this.searchTable.slice(firstIndex, lastIndex);
      }
    },
    searchTable() {
      const filterTable = new RegExp(this.search, "i");
      return this.theData.filter(el =>
        Object.keys(el).some(x => String(el[x]).match(filterTable))
      );
    }
  }
};
</script>

<style lang="scss"></style>
