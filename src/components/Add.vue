<template lang="pug">
  .add.container
    alert(v-if='alert', v-bind:message='alert')
    h1.page-header Add Customer
    form(v-on:submit='addCustomer')
      .well
        h4 Customer Info
        .form-group
          label First Name
          input.form-control(type='text', maxlength='20', placeholder='First Name', v-model='customer.FirstName', required='')
        .form-group
          label Initial
          input.form-control(type='text', maxlength='1', placeholder='Initial (optional)', v-model='customer.Initial')
        .form-group
          label Last Name
          input.form-control(type='text', maxlength='50', placeholder='Last Name', v-model='customer.LastName', required='')
      .well
        h4 Customer Contact
        .form-group
          label Email
          input.form-control(type='text', maxlength='50', placeholder='Email', v-model='customer.Email', required='')
        .form-group
          label Phone
          input.form-control(type='text', maxlength='8', placeholder='Phone', v-model='customer.Phone', required='')
      .well
        h4 Customer Location
        .form-group
          label Address
          input.form-control(type='text', maxlength='50', placeholder='Address', v-model='customer.Address', required='')
        .form-group
          label City
          input.form-control(type='text', maxlength='20', placeholder='City', v-model='customer.City', required='')
        .form-group
          label State
          input.form-control(type='text', maxlength='2', placeholder='State', v-model='customer.State', required='')
        .form-group
          label Zip Code
          input.form-control(type='text', maxlength='5', placeholder='Zip Code', v-model='customer.ZipCode', required='')
      button.btn.btn-primary(type='submit') Submit
</template>

<script>
    import Alert from './Alert'
    export default {
        name: 'add',
        data () {
            return {
            customer: {},
            alert:''
            }
        },
        methods: {
            addCustomer(e){
                if(!this.customer.FirstName || !this.customer.LastName || !this.customer.Email){
                    this.alert = 'Please fill in all required fields';
                } else {
                    let newCustomer = {
                        CustomerID: 0,
                        FirstName: this.customer.FirstName,
                        Initial: this.customer.Initial,
                        LastName: this.customer.LastName,
                        Phone: this.customer.Phone,
                        Email: this.customer.Email,
                        Address: this.customer.Address,
                        City: this.customer.City,
                        State: this.customer.State,
                        ZipCode: this.customer.ZipCode
                    }

                    this.$http.post('https://vcustomers-api.azurewebsites.net/api/customers/', newCustomer)
                        .then(function(response){
                            this.$router.push({path: '/', query: {alert: 'Customer Added'}});
                        });

                    e.preventDefault();
                }
                e.preventDefault();
            }
        },
        components: {
            Alert
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
