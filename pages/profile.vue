<template>
    <div class="container">
        <div class="row">
            <div class="col">
            <h1>Hello, <b>Admin</b>.</h1>
            Your current consumption: {{this.consumption}}  kWh 
            </div>
        </div>
        <div class="row">
            <div class="col">
            <b>Your Devices: </b>
                <div class="p-2" v-for="device, index in devices" :key="index">
                    <p>
                        {{index + 1}} - {{device.Title}} - {{device.Certificate}} 
                        <b-button v-if="device.Certificate == 'No Certificate'" @click="selectedDevice = device.Title" v-b-modal.modal-1 size="sm">Issue Certificate</b-button>
                        <b-button v-if="device.Certificate != 'No Certificate'" @click="setCertificate(device.Title)" v-b-modal.modal-2 size="sm">See Certificate</b-button>
                    </p>
                    <p>Current Production: {{device.Production}} kWh</p>
                    
            </div>
            </div>
        </div>
        <div class="row">
            
            * <i> IoT Devices will automatically track your production and consumption and if issued a certificate, input orders on the marketplace accordingly. </i>
        </div>

    <!-- Issue Certificate Modal </-->
    <b-modal ok-title="Issue Certificate" @ok="issueCertificate(selectedDevice)" header-bg-variant="dark" header-text-variant="light" ok-variant="success" cancel-variant="danger" id="modal-1" title="Issue Certificate">
    <div class="container text-center">
        <div class="row p-2 mb-2">
            <div class="col">
            <b>Certficiate Identity</b>  
                <b-form-select v-model="selectedIdentity" :options="options"></b-form-select>
            </div>
        </div>
        <div class="row">
            <div class="col">
             <b-form-checkbox v-b-tooltip title="Allows the IoT device to automatically make sell orders on your behalf.">Sell Rights</b-form-checkbox>
            </div>
            <div class="col">
            <b-form-checkbox v-b-tooltip title="Allows the IoT device to automatically make buy orders on your behalf.">Buy Rights</b-form-checkbox>
            </div>
        </div>
    </div>
  </b-modal>
  <!-- See Certificate Modal </-->
   <b-modal header-bg-variant="dark" header-text-variant="light" ok-variant="success" cancel-variant="danger" id="modal-2" title="See Certificate">
    <div class="container">
      <div class="row">
          <div class="col">
              <b>Certificate Issuer:</b> {{this.selectedCertificate}}
          </div>
      </div>
      <div class="row">
          <div class="col">
              <b>Issued At:</b> {{this.selectedCertificateDate}}
          </div>
      </div>

    </div>
  </b-modal>

    </div>
</template>

<script>
export default {
    data() {
        return {
            selectedIdentity: "Select Identity",
            selectedCertificateDate: "",
            selectedCertificate: "",
            selectedDevice: "",
            consumption: 0,
            devices: [
            {
                Title: "Suncell IoT Device",
                Certificate: "No Certificate",
                CertificateDate: "",
                Production: 200,
            },
            {
                Title: "Windmill IoT Device",
                Certificate: "No Certificate",
                CertificateDate: "",
                Production: 300,
            }
            ],
            options: [
                "Thomas Finch Rasmussen",
                "Tobias Sztuk Ahrenschneider",
                "Jonas Støve Rasmussen"
            ]
        }
    }, 
    mounted() {
      setInterval(() => {
        this.consumption = Math.floor(Math.random() * 10);
      }, 3000);
    },
    methods: {
        issueCertificate(title) {
           var deviceIndex = this.devices.findIndex((device => device.Title == title));
           this.devices[deviceIndex].Certificate = this.selectedIdentity;
           this.devices[deviceIndex].CertificateDate = new Date();
        },
        setCertificate(title) {
          var deviceIndex = this.devices.findIndex((device => device.Title == title));
          this.selectedDevice = title;
          this.selectedCertificate = this.devices[deviceIndex].Certificate;
          this.selectedCertificateDate = this.devices[deviceIndex].CertificateDate;
        }
    }
}
</script>


<style scoped>

</style>