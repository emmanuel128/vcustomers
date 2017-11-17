<template>
  <div class="details container">
      <br>
    <router-link to="/">Back</router-link>
    <h1 class="page-header">{{customer.FirstName}} {{customer.LastName}}
        <span class="pull-right">
            <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.CustomerID">Edit</router-link>
            <button class="btn btn-danger" v-on:click="deleteCustomer(customer.CustomerID)">Delete</button>
        </span>
    </h1>
    <ul class="list-group">
        <li class="list-group-item"><span class="glyphicon glyphicon-Phone" aria-hidden="true"></span> {{customer.Phone}}</li>
        <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span> {{customer.Email}}</li>
    </ul>

    <ul class="list-group">
        <li class="list-group-item">{{customer.Address}}</li>
        <li class="list-group-item">{{customer.City}}</li>
        <li class="list-group-item">{{customer.State}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
      customer: ''
    }
  },
  methods:{
      fetchCustomer(id){
          this.$http.get('https://vcustomers-api.azurewebsites.net/api/customers/'+id)
          .then(function(response){
            this.customer = response.body;
          });
      },
      deleteCustomer(id){
          this.$http.delete('https://vcustomers-api.azurewebsites.net/api/customers/'+id)
          .then(function(response){
            this.$router.push({path: '/', query: {alert: 'Customer Deleted'}});
          });
      }
  },
  created: function(){
      this.fetchCustomer(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
