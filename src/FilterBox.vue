<template>
    <input type="search" @input="filterList" v-model="searchString" :placeholder="'Min '+this.min+' letters'">
</template>
<script>
    let filterBox = {
        install(Vue)
        {
            Vue.component('filter-box', filterBox);
        },
        props: {
            min: {
                type: Number,
                default: 3,
                validator(value) {
                    return value > 0;
                }
            }
        },
        data() {
            return {
                searchString: '',
                timer: null,
            };
        },
        methods: {
            filterList() {
                clearTimeout(this.timer);
                this.timer = setTimeout(this.callFilterCallback, 1000);
            },
            callFilterCallback() {
                if(this.searchString.length >= this.min || this.searchString.length == 0)
                {
                    this.$emit('input',this.searchString);
                    this.$emit('filter',this.searchString);
                }
            }
        },
    }

    export default filterBox;
</script>
