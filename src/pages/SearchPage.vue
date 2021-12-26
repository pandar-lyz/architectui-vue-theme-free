<template>
    <section class="baseSetting">
        <div style="padding: 70px">
            <h1 class="center">电影资源管理中心</h1>
        </div>

        <div class="inputStyle">
            <el-input
                placeholder="搜索相关的电影资源..."
                v-model="input"
                class="input-with-select"
                style="width: 800px"
            >
                <el-select v-model="select" slot="prepend" placeholder="请选择">
                    <el-option label="通过星期查询电影" value="0"></el-option>
                    <el-option label="通过年份查询电影" value="1"></el-option>
                    <el-option label="通过年月查询电影" value="2"></el-option>
                    <el-option
                        label="通过年份和季度查询电影"
                        value="3"
                    ></el-option>
                    <el-option label="通过电影名查询电影" value="4"></el-option>
                    <el-option label="通过导演查询电影" value="5"></el-option>
                    <el-option label="通过演员查询电影" value="6"></el-option>
                    <el-option
                        label="查找与某演员合作最频繁的导演"
                        value="7"
                    ></el-option>
                    <el-option
                        label="查找演员和导演之间的合作次数"
                        value="8"
                    ></el-option>
                    <el-option
                        label="通过电影类型查询电影"
                        value="9"
                    ></el-option>
                    <el-option
                        label="通过电影评分查询电影"
                        value="10"
                    ></el-option>
                    <el-option
                        label="查询用户评价积极的电影"
                        value="11"
                    ></el-option>
                    <el-option
                        label="查询用户评价消极的电影"
                        value="12"
                    ></el-option>
                    <el-option
                        label="通过演员查询参演电影类型"
                        value="13"
                    ></el-option>
                    <el-option
                        label="查找合作最频繁的演员"
                        value="14"
                    ></el-option>
                    <el-option
                        label="查找合作最频繁的演员和导演"
                        value="15"
                    ></el-option>


                </el-select>
                <el-button
                    slot="append"
                    icon="el-icon-search"
                    @click="search"
                ></el-button>
            </el-input>
        </div>
    </section>
</template>

<script>

import router from "@/router";
export default {
    data() {
        return {
            input: "",
            select: "",
        };
    },
    methods: {
        search() {
            // eslint-disable-next-line no-console
            console.log("调用了search函数");
            if (this.select === "0") {
                //todo:调用通过年份查询电影数量的接口
                this.handle_0();
            }
           else if (this.select === "1") {
                //todo:调用通过年份查询电影数量的接口
                this.handle_1();
            } else if (this.select === "2") {
                //todo:调用通过年月查询电影数量的接口（输入格式：2019-3）
                this.handle_2();
            } else if (this.select === "3") {
                //todo:调用通过年和季度查询电影数量的接口（输入格式：2019-3）
                this.handle_3();
            } else if (this.select === "4") {
                //todo:调用通过电影名查询版本数量的接口
                this.handle_4();
            } else if (this.select === "5") {
                //todo:调用通过导演查询电影数量的接口
                this.handle_5();
            } else if (this.select === "6") {
                //todo:调用通过演员查询电影数量的接口
                this.handle_6();
            } else if (this.select === "7") {
                //todo:调用查看演员之间合作数量的接口
                this.handle_7();
            } else if (this.select === "8") {
                //todo:调用查看演员和导演合作的数量的接口
                this.handle_8();
            } else if (this.select === "9") {
                //todo:调用通过电影类别查询电影数量的接口
                this.handle_9();
            } else if (this.select === "10") {
                //todo:调用通过电影的评分查询电影信息的接口
                this.handle_10();
            } else if (this.select === "11") {

                this.handle_11();
            } else if (this.select === "12") {

                this.handle_12();
            } else if (this.select === "13") {

                this.handle_13();
            } else if (this.select === "14") {

                this.handle_14();
            }  else if (this.select === "15") {

                this.handle_15();
            }   else {
                router.push({ name: "notFound" });
            }
        },
        //调用通过星期查询电影数量的接口
        handle_0() {

            this.$store.dispatch("global/countMovieByTime", {
                week:this.input
            });
        },
        //调用通过年份查询电影数量的接口
        handle_1() {
            console.log(this.input)
            this.$store.dispatch("global/countMovieByTime",{
                year:this.input
            });
        },
        //调用通过年月查询电影数量的接口
        handle_2() {
            let data = this.input.split("-");
            this.$store.dispatch("global/countMovieByTime", {
                year: data[0],
                month: data[1],
            });
        },
        //调用通过年和季度查询电影数量的接口
        handle_3() {
            let data = this.input.split("-");
            this.$store.dispatch("global/countMovieByTime", {
                year: data[0],
                quarter: data[1],
            });
        },
        //调用通过电影名查询版本数量的接口
        handle_4() {
            this.$store.dispatch("global/countFormatByName", {name: this.input});
        },
        //调用通过导演查询版本数量的接口
        handle_5() {
            this.$store.dispatch("global/countMovieByDirector", {name: this.input});
        },
        //调用通过演员查询版本数量的接口
        handle_6() {
            this.$store.dispatch("global/countMovieByActor", {name: this.input});
        },
        //调用通查看演员之间合作的数量的接口TODO:和后端对接格式
        handle_7() {
            this.$store.dispatch("global/getAMostFrequentD", {person1: this.input});
        },
        //调用通查看演员和导演之间合作的数量的接口(格式：导演 演员)TODO:和后端对接格式
        handle_8() {
            let data = this.input.split(" ");
            this.$store.dispatch("global/countCooperationDA", {
                aname: data[0],
                dname: data[1],
            });
        },
        //通过电影类别查询电影数量的接口
        handle_9() {
            this.$store.dispatch("global/countMovieByType", {type: this.input});
        },
        //通过电影的评分查询电影信息的接口
        handle_10() {
            this.$store.dispatch("global/getMovieMoreThanScore",{score: this.input});
        },
        //通过用户的评分情感分析查询电影信息(名称和分数)
        handle_11() {
            this.$store.dispatch("global/getMovieWithPostiveReview");
        },//通过用户的评分情感分析查询电影信息(名称和分数)
        handle_12() {
            this.$store.dispatch("global/getMovieWithNegativeReview");
        },//通过用户的评分情感分析查询电影信息(名称和分数)
        handle_13() {
            this.$store.dispatch("global/getTypeWithActor",{name: this.input});
        },
        handle_14() {
            this.$store.dispatch("global/getMostFrequentAA",);
        },
        handle_15() {
            this.$store.dispatch("global/getMostFrequentAD",);
        },

    },
    watch: {
        select: {
            handler(newValue) {
                console.log("select值修改了");
                this.$store.commit("global/SETSELECT", newValue);
            },
        },
        input:{
            handler(newValue) {
                this.$store.commit("global/SETINPUT", newValue);
        }
        }
    },
};
</script>

<style>
::-webkit-input-placeholder {
    color: saddlebrown;
    font-size: 16px;
}

.center {
    text-align: center;
    font-size: 56px;
}

.baseSetting {
    background: url("~@/assets/img/background.jpg") no-repeat center;
    background-size: cover;
    height: 100vh;
    color: #bd6944;
    font-family: "Ubuntu", "Ma Shan Zheng", cursive, sans-serif;
}

.inputStyle {
    width: 35%;
    margin: 80px auto auto;
}

.el-select .el-input {
    width: 230px;
}

.input-with-select .el-input-group__prepend {
    background-color: #fff;
}
</style>
