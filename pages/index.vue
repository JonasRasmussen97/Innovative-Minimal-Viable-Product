<template>
  <div class="container">
    <div class="row">
      <div class="col text-center">
        <h2 class="p-2">Marketplace</h2>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <b-table thead-class="bg-dark text-white" :fields="fields" :items="marketplace">

          <!-- A custom formatted column -->
      <template #cell(title)="data">
        <b class="text-info">{{ data.value}}</b>
      </template>

       <template #cell(#)>
        <b-button>Purchase</b-button>
      </template>

        </b-table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      marketplace: [
        {
          Title: "Tesla Battery",
          Energy: "30 kWh",
          Price: "1000 DKK",
          Seller: "Admin",
        },
        {
          Title: "Sun Energy",
          Energy: "30 kWh",
          Price: "1000 DKK",
          Seller: "Admin",
        },
      ],
      fields: [
        "Title", "Energy", "Price", "Seller", "#"
      ]
    }
  }
}
</script>
