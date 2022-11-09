<template>
    <div>
        <h1>Countries List</h1>
        <div v-for="country in sortedArray.slice(0, 20)" :key="country.id">
            <p>{{country.Country}}</p>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    name:"CountriesList",
    data() {
        return {
            content: []
        }
    },
    computed: {
        sortedArray: function() {
            function compare(a, b) {
            if (a.TotalConfirmed > b.TotalConfirmed)
                return -1;
            if (a.TotalConfirmed < b.TotalConfirmed)
                return 1;
            return 0;
            }
            return this.content.slice().sort(compare);
            
        }
    },
    mounted()
    {
        axios.get('https://api.covid19api.com/summary')
        .then((response) => {
            this.content = response.data.Countries
        })
    },
}
</script>