<template>
    <div>
        <div class="content_item">
            <p>所在省：</p>
            <input type="text" onfocus=this.blur()>
            <picker class="pickerchange" @change="provinceChange" :value="index" :range="proviceArray">
                <view class="picker">
                    <!--  gradechanged  初始值赋值-->
                    &nbsp;&nbsp;{{provicechanged}}
                </view>
            </picker>
            <img class="arrow" src="/static/componentTitle/jiantou.png" alt="">
        </div>
        <div class="content_item">
            <p>所在市：</p>
            <input type="text" onfocus=this.blur()>
            <picker class="pickerchange" @change="cityPickerChange" :value="cityindex" :range="cityArray">
                <view class="picker">
                    <!--  gradechanged  初始值赋值 -->
                    &nbsp;&nbsp;{{citychanged}}
                </view>
            </picker>
            <img class="arrow" src="/static/componentTitle/jiantou.png" alt="">
        </div>
        <div class="content_item">
            <p>所在区/县：</p>
            <input type="text" onfocus=this.blur()>
            <picker class="pickerchange" @change="quPickerChange" :value="quindex" :range="quArray">
                <view class="picker">
                    <!--  gradechanged  初始值赋值-->
                    &nbsp;&nbsp;{{quchanged}}
                </view>
            </picker>
            <img class="arrow" src="/static/componentTitle/jiantou.png" alt="">
        </div>
    </div>
</template>

<script>
import { provice } from '../assets/city.js'
export default {
    data() {
        return {
            index: 1,
            areaArray: [],
            index: 1,
            cityindex: 1,
            quindex: 1,
            areaArray: [],
            provicechanged: '请选择',
            citychanged: '请选择',
            quchanged: '请选择',
            proviceArray: [],
            cityArray: [],
            quArray: [],
            person_show: false,
             titleList: {
                province: '请输入',
                city: '请输入',
                area: '请输入',
                name: '  ' + '请输入',
                phone: '  ' + '请输入',
                school: '  ' + '请输入',
                year: '请选择',
                gradeId: '请选择',
                classId: '请选择',
                teacher: '  ' + '请输入 ',
                teacherPhone: '  ' + '请输入'
            },
            dataList: [],
            mune_list: [{

            }],

        }
    },
    mounted() {
        this.areaArray = provice
        for (let i = 0; i < this.areaArray.length; i++) {
            this.proviceArray.push(this.areaArray[i].name)
        }
        console.log(this.proviceArray)
    },
    methods: {
        provinceChange(e) {
            // 选择省的时候清空市和区
            this.citychanged = ''
            this.quchanged = ''
            this.index = e.mp.detail.value
            // 找到点击的省的名字
            this.provicechanged = this.proviceArray[this.index]

            this.titleList.province = this.provicechanged
            console.log(this.index)
            // 找到省下面所有市
            let cityarray = this.areaArray[this.index].city
            // 重新选择省的时候清空市和区
            this.cityArray = []
            this.quArray = []
            // 循环把市的名字赋值
            for (let i = 0; i < cityarray.length; i++) {
                this.cityArray.push(cityarray[i].name)
            }
            console.log(this.cityArray)
            switch (this.provicechanged) {
                case '澳门':
                    this.citychanged = '澳门特别行政区'
                    this.titleList.city = this.citychanged
                    this.quarray = this.areaArray[32].city
                    this.quArray = this.quarray[0].districtAndCounty
                    this.quchanged = '澳门特别行政区'
                    break;
                case '香港':
                    this.citychanged = '香港特别行政区'
                    this.titleList.city = this.citychanged
                    this.quarray = this.areaArray[31].city
                    this.quArray = this.quarray[0].districtAndCounty
                    break;
                case '上海市':
                    this.citychanged = '上海市'
                    this.titleList.city = this.citychanged
                    this.quarray = this.areaArray[2].city
                    this.quArray = this.quarray[0].districtAndCounty
                    break;
                case '北京市':
                    this.citychanged = '北京市'
                    this.titleList.city = this.citychanged
                    this.quarray = this.areaArray[0].city
                    this.quArray = this.quarray[0].districtAndCounty
                    break;
                case '重庆市':
                    this.citychanged = '重庆市'
                    this.titleList.city = this.citychanged
                    this.quarray = this.areaArray[3].city
                    this.quArray = this.quarray[0].districtAndCounty
                    break;
                case '天津市':
                    this.citychanged = '天津市'
                    this.titleList.city = this.citychanged
                    this.quarray = this.areaArray[1].city
                    this.quArray = this.quarray[0].districtAndCounty
                    break;
                case '台湾省':
                    this.citychanged = '台湾省'
                    this.quchanged = '台湾省'
                    break;
                default:
                    break;
            }
        },
        cityPickerChange(e) {
            // 选择市的时候清空区
            this.quchanged = ''
            this.cityindex = e.mp.detail.value
            // 找到市的名字
            this.citychanged = this.cityArray[this.cityindex]
            this.titleList.city = this.citychanged
            // 找到下面所有的区
            let quarray = this.areaArray[this.index].city
            console.log(this.cityindex)
            console.log(quarray)
            // 把区的名字赋值
            this.quArray = quarray[this.cityindex].districtAndCounty

            console.log(this.quArray)
            //    this.cityArray = []
        },
        quPickerChange(e) {
            this.quindex = e.mp.detail.value
            this.quchanged = this.quArray[this.quindex]
            this.titleList.area = this.quchanged
            //    this.quArray = []
        },
    }
}
</script>

<style lang="less" scoped>
.content_item {
    display: flex;
    flex-direction: row;
    position: relative;
    margin-top: 10px; // justify-content: center;
    font-size: 16px;
    color: #64B4FF;
    .pickerchange {
        position: absolute;
        display: block;
        width: 139px;
        text-align: left;
        right: 0px;
        z-index: 100;
        color: #64B4FF; // border: 1px solid black;
        height: 27px;
    }
    .arrow {
        position: absolute;
        width: 8px;
        height: 6px;
        right: 20px;
        top: 10px;
    }
    input {
        position: relative;
        height: 27px; // background: rgba(179, 248, 255, 1);
        background: #FFFFFF;
        box-shadow: 0px 2px 5px 0px rgba(0, 0, 0, 0.13);
        border-radius: 2px; // text-align: left;
        width: 139px;
        text-align: left;
    }
    p {
        line-height: 27px;
        font-size: 16px;
        font-family: PingFangSC-Semibold;
        font-weight: bold;
        color: rgba(0, 99, 192, 1);
        text-align: left;
        width: 120px;
    }
}
</style>
