# @mathewparet/vue-filter-box

> A Vue.Js filter box to initiate search based on filter.

## Installation

``` bash
npm install @mathewparet/vue-filter-box
```

## Global Initialization

``` js
import Vue from 'vue;
import FilterBox from '@mathewparet/vue-filter-box';
Vue.use(FilterBox);
```

## Local Initialization

``` js
import FilterBox from '@mathewparet/vue-filter-box';
export default {
    components: {
        FilterBox,
    }
}
```

## Usage

``` html
<template>
    <div>
        <filter-box class="form-control form-control-sm" @filter="loadData" v-model="searchKey"></filter-box>
    </div>
</template>
<script>
    export default {
        data()
        {
            return {
                searchKey: '', 
                results: [],
            }
        }
        mounted()
        {
            this.loadData();
        }
        methods: {
            loadData(filterString=null)
            {
                // the function argument filterString will also have the filter string. You can use wither that or the v-model.
                
                let filter = this.filterString == null ? '' : this.filterString;

                axios.get(`/api/countries?filter=${filter}`)
                    .then(response => this.results = response.data);
            }
        }
    }
</script>
```

