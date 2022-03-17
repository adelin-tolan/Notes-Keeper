<template>
  <v-data-table
    :headers="headers"
    :items="groceryList"
    :items-per-page="10"
    class="elevation-1 mb-6"
  >
    <template #[`item.isPurchased`]="{ item }">
      <v-icon
        size="24px"
        :style="{ color: item.isPurchased ? 'green' : 'red' }"
      >
        mdi-{{ item.isPurchased ? "check" : "close" }}
      </v-icon>
    </template>
  </v-data-table>
</template>

<script>
export default {
  name: "MainGroceryListContent",
  data() {
    return {
      headers: [
        {
          text: "Product",
          align: "start",
          value: "name",
        },
        {
          text: "Quantity",
          value: "quantity",
        },
        {
          text: "Unit",
          value: "unitMeasure",
        },
        {
          text: "Purchased",
          value: "isPurchased",
        },
      ],
      groceryList: [],
    };
  },
  created() {
    fetch("https://mocki.io/v1/4a100cdb-3497-45d4-94b5-5c0e7cd951db")
      .then((response) => response.json())
      .then((data) => (this.groceryList = data))
      .catch((err) => console.error(err));
  },
};
</script>

<style></style>
