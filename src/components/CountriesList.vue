<template>
    <div class="container">
        <h1 class="header">Top 20 countries ordered descending by Cov-19 confirmed cases</h1>
        <ul class="list-group" v-for="country in sortedArray.slice(0, 20)" :key="country.id">
            <li>{{country.Country}}</li>
            <hr/>
        </ul>
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
<style scoped>
.list-group{
    list-style: none;
    align-items: center;
}

.list-group > li{
    font-size: larger;
}

.list-group > hr{
    margin-bottom: 18px;
    margin-top: 4px;
    width: 20rem;
}

.header {
    margin-bottom: 3rem;
}

.container{
    width: 40%;
}
</style>