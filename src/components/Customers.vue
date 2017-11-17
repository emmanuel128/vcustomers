<template lang="pug">
  .customers.container
    br
    Alert(v-if="alert", v-bind:message="alert")
    h1.page-header Manage Customers
    input(placeholder="Enter Name", v-model="filterInput").form-control
    br
    .table-responsive
      table.table.table-striped
        thead
          tr  
            th First Name
            th Last Name
            th Email
            th 
        tbody
          tr(v-for="customer in filterBy(customers, filterInput)")
            td {{customer.FirstName}}
            td {{customer.LastName}}
            td {{customer.Email}}
            td 
              router-link(v-bind:to="'/customer/'+customer.CustomerID").btn.btn-default View

</template>
<script>
  import Alert from './Alert';
  export default {
    name: 'customers',
    data () {
      return {
        customers: [],
        alert:'',
        filterInput:''
      }
    },
    methods: {
      fetchCustomers(){
        this.$http.get('https://vcustomers-api.azurewebsites.net/api/customers')
          .then(function(response){
            this.customers = response.body;
          });
      },
      filterBy(list, value){
        value = value.toUpperCase();
        return list.filter(function(customer){
          return customer.FirstName.toUpperCase().includes(value) ||
                 customer.LastName.toUpperCase().includes(value) ||
                 customer.Email.toUpperCase().includes(value)
          // return ( customer.LastName.toUpperCase().indexOf(value) || customer.FirstName.toUpperCase().indexOf(value) ) > -1;
        });
      }
    },
    mounted: function(){
      if(this.$route.query.alert){
        this.alert = this.$route.query.alert;
      }
      this.fetchCustomers();
    },
    updated: function(){
      // this.fetchCustomers();
    },
    components: {
      Alert
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
