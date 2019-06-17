<template>
    <div class="box">
        <div class="box-body">
            <input type="text" v-model="formatedmount">
        </div>
    </div>
</template>

<script>
import { isArray } from 'util';
    export default {
        mounted() {
            console.log('Component mounted.')
        },
        data: () => ({
            mount: 0,
            formatedmount: ''
        }),
        watch: {
            formatedmount: function(){
                let num = this.formatedmount.replace(/[^0-9,]/g, "")
                                            .replace(/(,.*?),(.*,)?/, "$1");
                let parts = num.split(',');
                let realNumber = (parts.length > 1 ? parseFloat(parts.join('.')) : parseInt(parts[0]));
                this.mount = (!realNumber ? 0 : realNumber);
                parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ".");
                if(parseInt(parts[1]) == 0) this.formatedmount = parts[0];
                this.formatedmount = parts.length > 1 ? parts.join(',') : parts[0];

                console.log(this.mount);
            }
        }

    }
</script>