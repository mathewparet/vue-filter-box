<template>
    <input type="search" @input="filterList" :value="this.value" :placeholder="'Min '+this.min+' letters'">
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
            },
            value: {
                required: false,
            }
        },
        data() {
            return {
                timer: null,
            };
        },
        watch: {
            value: {
                handler()
                {
                    if(this.value.length >= this.min || this.value.length === 0)
                        this.$emit('filter',this.value);
                },
                immediate: true,
            }
        },
        methods: {
            filterList(e) 
            {
                if(e.target.value.length === 0)
                    this.callFilterCallback();
                else if(e.target.value.length >= this.min)
                {
                    if(this.timer)
                        clearTimeout(this.timer);
                    this.timer = setTimeout(this.callFilterCallback, 1000, e.target.value);
                }
            },
            callFilterCallback(value='') 
            {
                if(value.length >= this.min || value.length == 0)
                {
                    this.$emit('input',value);
                }
            }
        },
    }

    export default filterBox;
</script>
