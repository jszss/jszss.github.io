---
title: 'canvas 线条动画'
date: 2021-06-07 12:03:02
tags: [canvas]
published: true
hideInList: false
feature: 
isTop: false
---
```js
<template>
    <div class="ceshi" @click="ceshi()">
        <run-line-canvas v-model="showIndex" class="canvas-set" :width="102" :height="600" :option="option"></run-line-canvas>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                option: {
                    speed: 5,
                    tailLine: {
                        length: 0.98,
                        moveColor: 'red',
                        shadowBlur: 1,
                        radius: 5,
                        tailColor: 'orange'
                    },
                    series: [
                        {
                            data: [
                                [4, 540],
                                [38, 540],
                                [48, 530],
                                [48, 30],
                                [78, 10],
                                [102, 10],
                                [600, 100],
                            ]
                        }
                    ]
                },
                showIndex: null
            }
        },
        mounted() {
            this.showIndex = 0;
            setinterval(function(){this.ceshi()},1000)
        },
        methods: {
            ceshi() {
                this.showIndex = 0;
            }
        }
    }
</script>
<style>
    body{
        .ceshi{
            cursor: pointer;
            color: rgb(30, 94, 54);
        }
    }
</style>
```
```js
 <template>
    <div>
        <canvas ref="myCanvas" :width="width" :height="height" class="all100"></canvas>
    </div>
</template>

<script>
export default {
    name: 'RunLineCanvas',
    model: {
        prop: 'sendRun',
        event: 'reback'
    },
    props: {
        // 绘制canvas逻辑宽度
        width: {
            type: Number,
            default: null
        },
        // 绘制canvas逻辑高度
        height: {
            type: Number,
            default: null
        },
        // 传入的参数配置以及线条数据
        option: {
            type: Object,
            default: null
        },
        // 控制点运动
        sendRun: {
            type: Number,
            default: null
        }
    },
    data() {
        return {
            // 判断是否重复绘制
            isReDraw: false,
            // canvas对象
            canvas: null,
            // canvas 2D对象
            ctx: null,
            // 线条数据
            lineData: [],
            // 基础配置
            canvasOption: {
                color: '#3d7ab9',
                width: 2,
                speed: 5,
                // 运动点配置参数
                tailLine: {
                    length: 0.95, // 该参数无法单独配置
                    moveColor: '#ff8d68',
                    shadowBlur: 2,
                    radius: 3,
                    tailColor: '#ff8d68'
                },
                // 线条两头的样式
                lineCap: {
                    type: 'circle',
                    size: 5,
                    show: true
                }
            },
            // 动画list数组
            runList: [],
            // 正在动画的线
            runningLine: 0,
            // 每一个动画的临时存贮
            chooseCheckTime: []
        };
    },
    computed: {
        /**
         * 计算两个点之间的距离
         * @returns {function(*, *): number}
         */
        getDistance() {
            return function getDistance(p1, p2) {
                return Math.sqrt((p1[0] - p2[0]) * (p1[0] - p2[0]) + (p1[1] - p2[1]) * (p1[1] - p2[1]));
            };
        }
    },
    mounted() {
        this.canvasCreate();
        this.$watch('option', () => {
            if (this.option.series && this.option.series.length > 0) {
                this.seriesDataDue();
                this.drawlineRun();
            }
        }, { immediate: true });
        this.$watch('sendRun', () => {
            if (this.sendRun !== null) {
                this.addNewRun(this.sendRun);
                this.$emit('reback', null);
            }
        }, { immediate: true });
    },
    beforeDestroy() {
        this.drawlineRun = () => {};
    },
    methods: {
        /**
         * 数据初始化，给每一条线赋予参数
         */
        seriesDataDue() {
            this.runList.splice(0);
            const object = JSON.parse(JSON.stringify(this.option));
            delete object.series;
            this.canvasOption = Object.assign(this.canvasOption, object, true);
            this.option.series.forEach((item, index) => {
                this.option.series[index] = Object.assign(this.canvasOption, this.option.series[index], true);
            });
            this.lineData = this.option.series;
        },
        /**
         * 页面初始化渲染canvas对象
         */
        canvasCreate() {
            this.canvas = this.$refs.myCanvas;
            this.ctx = this.canvas.getContext('2d');
        },
        /**
         * 通过传入数据进行线条绘制
         */
        drawLine() {
            this.lineData.forEach((line, index) => {
                this.ctx.beginPath();
                this.ctx.strokeStyle = line.color;
                this.ctx.lineWidth = line.width;
                line.data.forEach((point, index) => {
                    if (index === 0) {
                        this.ctx.moveTo(point[0], point[1]);
                    } else {
                        this.ctx.lineTo(point[0], point[1]);
                    }
                });
                this.ctx.stroke();
                this.lineCapCheck(line);
                if (this.runList.length === 0) {
                    this.moveLineData(line);
                }
            });
        },

        /**
         * 线条两头样式处理
         * @param line
         */
        lineCapCheck(line) {
            const lineCapData = {
                color: line.color,
                data: line.data,
                lineCap: line.lineCap
            };
            if (lineCapData.lineCap.show) {
                this[`LineCap${lineCapData.lineCap.type}`](lineCapData);
            }
        },

        /**
         * 线条两端圆形样式
         * @constructor
         */
        LineCapcircle(lineCapData) {
            const moveList1 = this.mathMove(lineCapData.data[0], lineCapData.data[1], lineCapData.lineCap.size);
            const moveList2 = this.mathMove(lineCapData.data[lineCapData.data.length - 1], lineCapData.data[lineCapData.data.length - 2], lineCapData.lineCap.size);
            // 画线开始圆
            this.ctx.beginPath();
            this.ctx.arc(lineCapData.data[0][0] + moveList1[0], lineCapData.data[0][1] + moveList1[1], lineCapData.lineCap.size, 0, Math.PI * 2, true);
            this.ctx.stroke();
            this.ctx.fillStyle = lineCapData.color;
            this.ctx.fill();
            // 画线结束圆
            this.ctx.beginPath();
            this.ctx.arc(lineCapData.data[lineCapData.data.length - 1][0] + moveList2[0], lineCapData.data[lineCapData.data.length - 1][1] + moveList2[1], lineCapData.lineCap.size, 0, Math.PI * 2, true);
            this.ctx.stroke();
            this.ctx.fillStyle = lineCapData.color;
            this.ctx.fill();
        },

        /**
         * 计算点位头部位置计算
         * @param ponit1
         * @param point2
         * @param size
         * @returns {[number, number]}
         */
        mathMove(ponit1, point2, size) {
            const bigSize = Math.pow((Math.pow(point2[0] - ponit1[0], 2) + Math.pow(point2[1] - ponit1[1], 2)), 1 / 2) / size;
            const movex = (point2[0] - ponit1[0]) / bigSize;
            const movey = (point2[1] - ponit1[1]) / bigSize;
            return [movex, movey];
        },

        /**
         * 动画数据数组处理
         * @param data
         */
        moveLineData(series) {
            const pointList = [];
            for (var i = 0; i < series.data.length; i++) {
                var start = series.data[i];
                var end = series.data[i + 1];
                if (start && end) {
                    var distance = Math.floor(this.getDistance(start, end));
                    var vx = (end[0] - start[0]) / distance;
                    var vy = (end[1] - start[1]) / distance;
                    for (var j = 0; j < distance; j++) {
                        pointList.push([start[0] + vx * j, start[1] + vy * j]);
                    }
                }
            }
            series.data = pointList;
            this.runList.push(series);
        },

        /**
         * 绘制移动点
         */
        drawlineRun() {
            let runNum = 0;
            this.ctx.fillStyle = `rgba(0,0,0,${this.canvasOption.tailLine.length})`;
            const prev = this.ctx.globalCompositeOperation;
            this.ctx.globalCompositeOperation = 'destination-in';
            this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height);
            this.ctx.globalCompositeOperation = prev;
            this.ctx.shadowColor = '';
            this.ctx.shadowBlur = 0;
            this.drawLine();
            this.chooseCheckTime.forEach((item, index) => {
                if (this.runList[item.index].data.length >= item.runIndex) {
                    this.drawPoint(item.runIndex, item.index);
                    this.chooseCheckTime[index].runIndex += this.runList[item.index].speed;
                    runNum++;
                }
            });
            if (runNum === 0 && this.isReDraw) {
                this.ctx.shadowColor = '';
                this.ctx.shadowBlur = 0;
                this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
                this.drawLine();
                this.isReDraw = false;
            } else {
                this.isReDraw = true;
            }
            requestAnimationFrame(this.drawlineRun.bind(this));
        },

        /**
         * 动画绘点函数
         * @param checkLength
         * @param index
         */
        drawPoint(checkLength, index) {
            this.ctx.shadowColor = this.runList[index].tailLine.moveColor;
            this.ctx.shadowBlur = this.runList[index].tailLine.shadowBlur;
            this.ctx.beginPath();
            this.ctx.arc(this.runList[0].data[checkLength - 1][0], this.runList[0].data[checkLength - 1][1], this.runList[index].tailLine.radius, 0, Math.PI * 2);
            this.ctx.stroke();
            this.ctx.fillStyle = this.runList[index].tailLine.tailColor;
            this.ctx.fill();
        },

        /**
         * 新动画创建(动画触发)
         * @param index
         */
        addNewRun(index) {
            this.chooseCheckTime.push({ index: index, runIndex: 1 });
        }
    }
};
</script>

<style scoped>

</style>

```