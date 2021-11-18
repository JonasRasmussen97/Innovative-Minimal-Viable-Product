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

       <template #cell(#)="data">
         <div v-if="data.item.Type == 'Selling'">
        <b-button>Purchase</b-button>
         </div>
         <div v-if="data.item.Type == 'Buying'">
          <b-button>Sell</b-button>
         </div>
      </template>

        </b-table>
      </div>
    </div>
    <div class="row">
      <div class="col text-center">
      <b-button @click="$bvModal.show('order-modal')">Create Order</b-button>
      </div>
    </div>

    <!-- Create Order Modal <-->
     <b-modal 
     id="order-modal"
     title="Create Order"
     header-bg-variant="dark"
     header-text-variant="white"
     ok-title="Place Order"
     ok-variant="success"
     @ok="createOrder(orderEnergy, orderPrice, orderType, 'Admin')"
     >
    <div class="container">
      <div class="row">
        <div class="col">
    <b-dropdown id="dropdown-1" :text="this.orderType" class="mb-2">
    <b-dropdown-item v-model="orderType" @click="orderType = 'Buying'">Buy Order</b-dropdown-item>
    <b-dropdown-item v-model="orderType" @click="orderType = 'Selling'">Sell Order</b-dropdown-item>
    </b-dropdown>
    </div>
      </div>
      <div class="row">
        <div class="col">
    <p><b-input v-model="orderEnergy" :state="orderEnergy.length > 0" placeholder="Enter order energy in kWh"></b-input></p>
    <p><b-input v-model="orderPrice" :state="orderPrice.length > 0" placeholder="Enter order price in DKK"></b-input></p>
    </div>
      </div>
    </div>
  </b-modal>


  </div>
</template>

<script>
export default {
  methods: {
    createOrder(Energy, Price, Type, Seller) {
      this.marketplace.push({
        Energy: Energy + ' kWh',
        Price: Price + ' DKK',
        Type: Type,
        Seller: Seller
      })
    }
  },
  data() {
    return {
      orderTitle: '',
      orderPrice: '',
      orderEnergy: '',
      orderType: 'Select Order Type',
      marketplace: [
        {
          Energy: "30 kWh",
          Price: "1000 DKK",
          Type: "Selling",
          Seller: "Admin",
        },
        {
          Energy: "30 kWh",
          Price: "1000 DKK",
          Type: "Buying",
          Seller: "Admin",
        },
      ],
      fields: [
        "Energy", "Price", {key: 'Type', sortable: true}, "Seller", "#"
      ]
    }
  }
}
</script>
