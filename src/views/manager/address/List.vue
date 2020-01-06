<template>
    <div>
        <briup-fulllayout title="常用地址">
            <van-list>
            <van-cell
                v-for="item in addresses"
                :key="item.id"
                :title="item.province+'   '+item.city+'   '+
                item.area+'   '+item.address"
            />
            </van-list>
            <van-address-list
            @add="toAddressEditHandler"
            />
            <!-- <van-button size="large" is-link to="address_edit">添加</van-button> -->
        </briup-fulllayout>
    </div>
</template>

<script>
import { get } from '../../../http/axios'
import { mapState } from 'vuex'
export default {
    data(){
        return{
            addresses:[]
        }
    },
    computed:{
        ...mapState("user",["info"])
    },
    created(){
        this.loadAddress();
    },
    methods:{
        loadAddress(){
            let id=this.info.id;
            let url="/address/findByCustomerId?id="+id;
            get(url).then((response)=>{
                this.addresses=response.data;
            })
        },
        toAddressEditHandler() {
            this.$router.push("/manager/address_edit");
        }
    }
}
</script>