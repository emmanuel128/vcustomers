<template lang="pug">
    .edit.container
        Alert(v-if="alert", v-bind:message="alert")
        h1.page-header Edit Customer
        form(v-on:submit="updateCustomer")
            .well
                h4 Customer Info
                .form-group
                    label First Name
                    input(type="text", maxlength="20", placeholder="First Name", v-model="customer.FirstName", required).form-control

                .form-group
                    label Initial
                    input(type="text", maxlength="1", placeholder="Initial (optional)", v-model="customer.Initial").form-control
                
                .form-group
                    label Last Name
                    input(type="text", maxlength="50", placeholder="Last Name", v-model="customer.LastName", required).form-control

            .well
                h4 Customer Contact
                .form-group
                    label Email
                    input(type="text", maxlength="50", placeholder="Email", v-model="customer.Email", required).form-control

                .form-group
                    label Phone
                    input(type="phone", maxlength="8", placeholder="Phone", v-model="customer.Phone", required).form-control
                
            .well
                h4 Customer Location
                .form-group
                    label Address
                    input(type="text", maxlength="50", placeholder="Address", v-model="customer.Address", required).form-control

                .form-group
                    label City
                    input(type="text", maxlength="20", placeholder="City", v-model="customer.City", required).form-control
                
                .form-group
                    label State
                    input(type="text", maxlength="2", placeholder="State", v-model="customer.State", required).form-control
                
                .form-group
                    label Zip Code
                    input(type="number", maxlength="5", placeholder="Zip Code", v-model="customer.ZipCode", required).form-control
                
            button(type="submit").btn.btn-primary Submit
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
        fetchCustomer(id){
            this.$http.get('https://vcustomers-api.azurewebsites.net/api/customers/'+id)
            .then(function(response){
                this.customer = response.body;
            });
        },
        updateCustomer(e){
            if(!this.customer.FirstName || !this.customer.LastName || !this.customer.Email){
                this.alert = 'Please fill in all required fields';
            } else {
                let updCustomer = {
                    CustomerID: this.customer.CustomerID,
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
                console.log("id:" + this.$route.params.id);
                console.log(updCustomer);
                this.$http.put('https://vcustomers-api.azurewebsites.net/api/customers/'+this.$route.params.id, updCustomer, {
                    headers:{
                        "Content-Type": "application/json"
                    }
                })
                .then(function(response){
                    console.log(response);
                    this.$router.push({path: '/', query: {alert: 'Customer Updated'}});
                });

                e.preventDefault();
            }
            e.preventDefault();
        }
    },
    created: function(){
        this.fetchCustomer(this.$route.params.id);
    },
    components:{
        Alert
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
