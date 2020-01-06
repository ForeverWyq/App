<template>
    <briup-fulllayout title="新增地址">
        <div>
            <van-cell-group>
                <van-field v-model="form.telephone" placeholder="手机号"/>
            </van-cell-group>
            <van-cell-group>
                <van-field v-model="form.province" placeholder="省"/>
            </van-cell-group>
            <van-cell-group>
                <van-field v-model="form.city" placeholder="市"/>
            </van-cell-group>
            <van-cell-group>
                <van-field v-model="form.area" placeholder="区"/>
            </van-cell-group>
            <van-cell-group>
                <van-field v-model="form.address" placeholder="详细地址"/>
            </van-cell-group>
            <van-button round type="primary" size="large" @click="submitHandler()">保存</van-button>
        </div>
    </briup-fulllayout>
</template>
<script>
import { mapState } from 'vuex';
import { post } from '../../../http/axios'
export default {
    data(){
        return{
            form:{}
        }
    },
    computed:{
        ...mapState('user',['info'])
    },
    methods:{
        submitHandler(){
            let url="/address/saveOrUpdate"
            this.form.customerId = this.info.id;
            post(url,this.form).then((response)=>{
                // 返回上一个页面
                this.$router.go(-1);
                this.$toast.success(response.message)
            })
        }
    }
}
</script>