<template>
    <div>
        <!--        //商品规格组件-->
        <van-popup v-if="isShowPec" v-model="isShowPec" position="bottom" round @click-overlay="closePop">
            <div class="pop">
                <div>
                    <van-row v-if="specList.length">
                        <van-col :span="8">
                            <img  class="popImg" :src="this.host+'/uploads/foodsDetail/'+specList[selectIndex].specImg" alt/>
                        </van-col>
                        <van-col :span="16">
                            <div class="topTitle">{{parentData.foodsName}}</div>
                            <div class="money">￥{{specList[selectIndex].specPrice}}</div>
                            <div class="kucun">{{specList[selectIndex].specStock}}库存件</div>
                        </van-col>
                    </van-row>
                </div>
                <div class="smillTitle">{{parentData.foodsSpecifications}}</div>
                <ul class="specList">
                    <li v-for="(item, index) in specList" @click="selectSpecIndex(index)" :class="[selectIndex==index?'active':null]" :key="index"
                    >{{item.specName}}
                    </li>
                </ul>
                <van-row style="margin-top:15px;margin-bottom:15px;">
                    <van-col :span="16">
                        <div style="font-size:16px;text-indent:12px;">
                            购买数量
                        </div>
                    </van-col>
                    <van-col :span="8" style="font-size:16px; ">
                        <van-stepper v-model="specNumber"/>
                    </van-col>
                </van-row>
                <van-button color="red" size="large" @click="closePop">确定</van-button>
            </div>
        </van-popup>
    </div>
</template>

<script>
    export default {
        name: "specShow",
        props: {
            specShow: {
                type: Boolean
            },
            // specImg: String,
            specList: Array,
            parentData: Object
        },
        data() {
            return {
                selectSpecContent: 0,
                specNumber: 1,
                isShowPec: false,
                selectIndex:0,
                selectSpec:{},
                showImg:'',
                showStock:'',
                showPrice:'',
                newSpecist:[]
            }
        },
        created() {

        },
        mounted() {

        },
        methods: {
            closePop() {
                this.$emit('closePop')
            },
            selectSpecIndex(index){
                console.log(index);
                this.selectIndex = index
            }

        },
        watch: {
            specShow(value) {
                this.isShowPec = value
            }
        }
    }
</script>
<style scoped lang="less">
    .pop {
        background: white;
        width: 100%;
        display: block;
        padding-top: 10px;
        text-align: left;
        border-radius: 15px;

        .kucun {
            font-size: 12px;
        }

        .topTitle {
            font-size: 17px;
        }

        .smillTitle {
            font-size: 12px;
            line-height: 20px;
            text-indent: 15px;
        }

        .money {
            color: red;
        }

        .popImg {
            width: 94%;
            margin-left: 2%;
            height: 90px;
        }

        .specList {
            display: flex;
            font-size: 15px;
            margin-top: 15px;

            li {
                background: #f2f3f5;
                color: black;
                border-radius: 20px;
                padding-left: 15px;
                padding-right: 15px;
                margin-left: 15px;
            }

            .active {
                background: #fef8f8;
                border: #ef4436 1px solid;
            }
        }
    }
</style>