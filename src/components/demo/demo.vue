<template>
    <div class="hello">
        <mt-header fixed title="固定在顶部"></mt-header>
        <h1>{{ msg }}</h1>

        <div class="aaa">

        </div>
        <div class="bbb">
            1像素边框
        </div>
        <mt-swipe :auto="4000">
            <mt-swipe-item class="slide1">1</mt-swipe-item>
            <mt-swipe-item class="slide2">2</mt-swipe-item>
            <mt-swipe-item class="slide3">3</mt-swipe-item>
        </mt-swipe>

        <div class="page-popup-wrapper">
            <mt-button @click.native="popupVisible1 = true" size="large" ref="button">中部弹出 popup</mt-button>
            <mt-button @click.native="popupVisible2 = true" size="large">上侧弹出 popup</mt-button>
            <mt-button @click.native="popupVisible3 = true" size="large">右侧弹出 popup</mt-button>
            <mt-button @click.native="popupVisible4 = true" size="large">下侧弹出 popup</mt-button>
        </div>
        <mt-popup v-model="popupVisible1" popup-transition="popup-fade" class="mint-popup-1" :style="{ top: buttonBottom + 10 + 'px' }">
            <h1>popup</h1>
            <p>/ ˈpɑpˌʌp /</p>
            <p>n. 弹出式; [棒]内野飞球; 自动起跳式装置</p>
            <p>adj. 弹起的; 有自动起跳装置的</p>
        </mt-popup>
        <mt-popup v-model="popupVisible2" position="top" class="mint-popup-2" :modal="false">
            <p>更新成功</p>
        </mt-popup>
        <mt-popup v-model="popupVisible3" position="right" class="mint-popup-3" :modal="false">
            <mt-button @click.native="popupVisible3 = false" size="large" type="primary">关闭 popup</mt-button>
        </mt-popup>
        <mt-popup v-model="popupVisible4" position="bottom" class="mint-popup-4">
            <mt-picker :slots="dateSlots" @change="onDateChange" :visible-item-count="5" :show-toolbar="false"></mt-picker>
        </mt-popup>

        <div class="box"></div>
    </div>

</template>

<script>
export default {
    name: "demo",
    data() {
        return {
            msg: "2x，3x背景图",
            popupVisible1: false,
            popupVisible2: false,
            popupVisible3: false,
            popupVisible4: false,
            buttonBottom: 0,
            dateSlots: [
                {
                    flex: 1,
                    values: [
                        "2016-01",
                        "2016-02",
                        "2016-03",
                        "2016-04",
                        "2016-05",
                        "2016-06"
                    ],
                    className: "slot1",
                    textAlign: "right"
                },
                {
                    divider: true,
                    content: "-",
                    className: "slot2"
                },
                {
                    flex: 1,
                    values: [
                        "2016-01",
                        "2016-02",
                        "2016-03",
                        "2016-04",
                        "2016-05",
                        "2016-06"
                    ],
                    className: "slot3",
                    textAlign: "left"
                }
            ]
        };
    },
    watch: {
        popupVisible2(val) {
            if (val) {
                setTimeout(() => {
                    this.popupVisible2 = false;
                }, 2000);
            }
        }
    },
    methods: {
        onDateChange(picker, values) {
            if (values[0] > values[1]) {
                picker.setSlotValue(1, values[0]);
            }
            this.dateStart = values[0];
            this.dateEnd = values[1];
        }
    },
    mounted() {
        this.buttonBottom = this.$refs.button.$el.getBoundingClientRect().bottom;
    }
};
</script>

<style scoped lang="less">
@import "../../common/less/main.less";
.hello {
    height: 1500px;
}

h1 {
    font-size: @font-size-h1;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: @theme-yellow;
}
.aaa {
    width: 90px;
    height: 96px;
    .bg-image("test");
    background-repeat: no-repeat;
    background-size: cover;
    margin: 0 auto;
}
.bbb {
    width: 100%;
    height: 96px;
    .border-1px(#f00);
    line-height: 96px;
    text-align: center;
    margin-bottom: 20px;
}

.mint-swipe {
    height: 200px;
    color: #fff;
    font-size: 30px;
    text-align: center;
    margin-bottom: 20px;
}
.mint-swipe-item {
    line-height: 200px;
}
.slide1 {
    background-color: #0089dc;
    color: #fff;
}
.slide2 {
    background-color: #ffd705;
    color: #000;
}
.slide3 {
    background-color: #ff2d4b;
    color: #fff;
}

.mint-popup-1 {
    width: 200px;
    border-radius: 8px;
    padding: 10px;
    transform: translate(-50%, 0);
    h1 {
        font-size: 20px;
        color: #26a2ff;
    }
    p {
        margin-bottom: 10px;
    }
}
.mint-popup-1::before {
    triangle: 10px top #fff;
    content: "";
    position: absolute;
    top: -20px;
    right: 50px;
}
.mint-popup-2 {
    width: 100%;
    height: 50px;
    text-align: center;
    background-color: rgba(0, 0, 0, 0.7);
    backface-visibility: hidden;
}
.mint-popup-2 p {
    line-height: 50px;
    color: #fff;
}
.mint-popup-3 {
    width: 100%;
    height: 100%;
    background-color: #fff;
}
.mint-popup-3 .mint-button {
    position: absolute;
    width: 90%;
    top: 50%;
    left: 5%;
    transform: translateY(-50%);
}
.mint-popup-4 {
    width: 100%;
    .picker-slot-wrapper,
    .picker-item {
        backface-visibility: hidden;
    }
}
.box{
    width: 2.3467rem;
    height: 2.3467rem;
    background: red;
}
</style>
