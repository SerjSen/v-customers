<template>
    <div class="customers container">
        <Alert v-if="alert" v-bind:message="alert"></Alert>
        <h1 class="page-header">Manage Customers</h1>
        <table class="table table-striped">
            <thead>
            <tr>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Email</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="customer in customers">
                <td>{{customer.first_name}}</td>
                <td>{{customer.last_name}}</td>
                <td>{{customer.email}}</td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    import Alert from './Alert';
    export default {
        name: 'customers',
        components: {
          Alert
        },
        data () {
            return {
                customers: [],
                alert: ''
            }
        },
        methods: {
            fetchCustomers(){
                this.$http.get('http://rest.loc/customers').then(function (response) {
                    this.customers = response.body;
                })
            }
        },
        created: function () {
            if (this.$route.query.alert) {
                this.alert = this.$route.query.alert;
            }
            this.fetchCustomers();
        },
        updated: function () {
            this.fetchCustomers();
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
