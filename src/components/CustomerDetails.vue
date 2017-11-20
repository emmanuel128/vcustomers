<template lang="pug">
    .details.container
        br
        router-link(to="/") Back
        h1.page-header {{customer.FirstName}} {{customer.LastName}}
            span.pull-right
                router-link.btn.btn-primary(v-bind:to="'/edit/' + customer.CustomerID") Edit
                button.btn.btn-danger(v-on:click="deleteCustomer(customer.CustomerID)") Delete
            
        ul.list-group
            li.list-group-item
                span.glyphicon.glyphicon-phone(aria-hidden="true") &nbsp{{customer.Phone}}
            li.list-group-item
                span.glyphicon.glyphicon-envelope(aria-hidden="true") &nbsp{{customer.Email}}

        ul.list-group
            li.list-group-item {{customer.Address}}
            li.list-group-item {{customer.City}}
            li.list-group-item {{customer.State}}
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
