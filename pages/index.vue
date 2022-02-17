<template>
    <div>
        <div>
            <a :href="`https://cataas.com${cat.url}`" target="_blank">
                <img :src="`https://cataas.com${cat.url}`" />
            </a>
        </div>

        <div>
            The population in {{ year }} was {{ population }}
        </div>

        <div>
            <p>{{ chuck.value.joke }}</p>

        </div>
    </div>
</template>

<script>
export default {
    name: 'IndexPage',
    async asyncData({ $axios }) {
        // cat api
        const cat = await $axios.$get('https://cataas.com/cat/says/hello,%20world?json=true&type=angry');

        // population api
        const year = 2016;
        const popData = await $axios.$get(`https://datausa.io/api/data?drilldowns=Nation&measures=Population&year=${year}`);

        // fav api
        const chuck = await $axios.$get('http://api.icndb.com/jokes/random');

        return {
            cat,
            year,
            population: popData.data[0].Population,
            chuck,
        };
    },
}
</script>
