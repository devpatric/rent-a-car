<template>
    <div class="employees">
        <div v-if="!isLoaded">
            <h3 class="text-center">Loading...</h3>
        </div>
        <div v-if="isLoaded">
            <clients-form></clients-form>

            <hr>

            <table-list :columns="tableColumns" :table-data="employees"></table-list>
        </div>
    </div>
</template>

<script>
    import ClientsForm from './Forms/ClientsForm.vue';
    import TableList from './../Views/TableList.vue';
    
    const tableColumns = ['Ord', 'Name', 'Identification', 'CreditCard', 'CreditLimit', 'PersonType', 'State', 'Actions'];
    
    export default {
        components: {
            TableList,
            ClientsForm
        },
        data() {
            return {
                tableColumns: [...tableColumns],
                isLoaded: false,
                employees: []
            };
        },
        mounted() {
            this.$axios.get('http://localhost:8000/api/employees')
                .then(res => {
                    this.employees = (res.status === 204) ? [] : res.data.slice(0);
                    this.isLoaded = true;
                });
        }
    };
</script>