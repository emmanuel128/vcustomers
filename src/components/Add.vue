<template>
  <div class="add container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Add Customer</h1>
    <form v-on:submit="addCustomer">
        <div class="well">
            <h4>Customer Info</h4>
            <div class="form-group">
                <label>First Name</label>
                <input type="text" class="form-control" maxlength="20" placeholder="First Name" v-model="customer.FirstName" required>
            </div>
            <div class="form-group">
                <label>Initial</label>
                <input type="text" class="form-control" maxlength="1" placeholder="Initial (optional)" v-model="customer.Initial">
            </div> 
            <div class="form-group">
                <label>Last Name</label>
                <input type="text" class="form-control" maxlength="50" placeholder="Last Name" v-model="customer.LastName" required>
            </div>
        </div>
        <div class="well">
            <h4>Customer Contact</h4>
            <div class="form-group">
                <label>Email</label>
                <input type="text" class="form-control" maxlength="50" placeholder="Email" v-model="customer.Email" required>
            </div>
            <div class="form-group">
                <label>Phone</label>
                <input type="text" class="form-control" maxlength="8" placeholder="Phone" v-model="customer.Phone" required>
            </div>
        </div>

        <div class="well">
            <h4>Customer Location</h4>
            <div class="form-group">
                <label>Address</label>
                <input type="text" class="form-control" maxlength="50" placeholder="Address" v-model="customer.Address" required>
            </div>
            <div class="form-group">
                <label>City</label>
                <input type="text" class="form-control" maxlength="20" placeholder="City" v-model="customer.City" required>
            </div>
            <div class="form-group">
                <label>State</label>
                <input type="text" class="form-control" maxlength="2" placeholder="State" v-model="customer.State" required>
            </div>
            <div class="form-group">
                <label>Zip Code</label>
                <input type="text" class="form-control" maxlength="5" placeholder="Zip Code" v-model="customer.ZipCode" required>
            </div>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
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
