<template>
  <div class="green-house">
    <div class="environment">
      <div class="environment-setting__header">
        <div class="header-item" :class="{ active: isActive === 1 }" @click="handleFoldWeather">
          <span class="header-item__key">天气：</span>
          <SvgIcon svg-name="sun" :size="16"></SvgIcon>

          <span class="header-item__value">晴天</span>
          <SvgIcon svg-name="fold" :size="16"></SvgIcon>
        </div>
        <span class="vertical-line">|</span>

        <div class="header-item" :class="{ active: isActive === 2 }" @click="handleFoldLighting">
          <span class="header-item__key">光照：</span>
          <SvgIcon svg-name="light" :size="16"></SvgIcon>

          <span class="header-item__value">自然光</span>
          <SvgIcon svg-name="fold" :size="16"></SvgIcon>
        </div>
        <span class="vertical-line">|</span>

        <div class="header-item" :class="{ active: isActive === 3 }" @click="handleFoldTime">
          <span class="header-item__key">时间：</span>
          <span class="header-item__value">15:20:40</span>
          <SvgIcon svg-name="fold" :size="16"></SvgIcon>
        </div>
      </div>
      <div v-if="isActive === 1" class="environment-setting__content">
        <div class="content-item">
          <span>天气设置</span>
          <SvgIcon svg-name="close" :size="16" @click="handleClose()"></SvgIcon>
        </div>
        <div class="content-item__detail">
          <div class="detail-left">
            <!-- <div v-for="(key, value) in weatherList" :key="value" class="detail-left__item" :class="{ active: activeMetric === value }" @click="handleMetricClicked(value)">
            <SvgIcon :svg-name="value" :size="16"></SvgIcon>
            <span class="detail-left__value"> {{ key }}</span>
          </div> -->
            <div v-for="(item, index) in weatherList" :key="index" class="detail-left__item" :class="{ active: index === activeIndex }" @click="handleMetricClicked(index)">
              <SvgIcon :svg-name="item.name" :size="16"></SvgIcon>
              <span class="detail-left__value"> {{ item.text }}</span>
            </div>
          </div>
          <div class="detail-right">
            <div class="params__formItem">
              <div class="params__formLabel">降雨量：</div>
              <div class="params__formInput">
                <el-input-number v-model="params.rainnum" controls-position="right" :min="0" :max="1000"></el-input-number>
              </div>
              <span class="params__formUnit">mm</span>
            </div>

            <div class="params__formItem">
              <div class="params__formLabel">降雪量：</div>
              <div class="params__formInput">
                <el-input-number v-model="params.snownum" controls-position="right" :min="0" :max="1000"></el-input-number>
              </div>
              <span class="params__formUnit">mm</span>
            </div>
            <div class="params__formItem">
              <div class="params__formLabel">云量：</div>
              <div class="params__formInput">
                <el-input-number v-model="params.cloudnum" controls-position="right" :min="0" :max="1000"></el-input-number>
              </div>
            </div>
            <div class="params__formItem">
              <div class="params__formLabel">雾量：</div>
              <div class="params__formInput">
                <el-input-number v-model="params.fognum" controls-position="right" :min="0" :max="1000"></el-input-number>
              </div>
            </div>
          </div>
        </div>
        <div class="content-item__button">
          <!-- <span class="button"> 取消</span> -->
          <el-button>取消</el-button>
          <el-button type="primary" @click="handleSubmit">确定</el-button>
          <!-- <span class="button"> 确定</span> -->
        </div>
      </div>
      <div v-if="isActive === 2" class="environment-setting__content">
        <div class="content-item">
          <span>光照设置</span>
          <SvgIcon svg-name="close" :size="16" @click="handleClose()"></SvgIcon>
        </div>
        <div class="content-item__detail">
          <div class="detail-left">
            <div v-for="(item, index) in lightingList" :key="index" class="detail-left__item" :class="{ active: index === activeIndex }" @click="handleMetricClicked(index)">
              <SvgIcon :svg-name="item.name" :size="16"></SvgIcon>
              <span class="detail-left__value"> {{ item.text }}</span>
            </div>
          </div>
          <div class="detail-right">
            <div class="params__formItem">
              <div class="params__formLabel">光源颜色：</div>
              <div class="params__formInput">
                <el-select v-model="lightColor" placeholder="红色光">
                  <el-option label="红色光" value="0"></el-option>
                  <el-option label="绿色光" value="1"></el-option>
                  <el-option label="蓝色光" value="2"></el-option>
                </el-select>
                <!-- <el-dropdown trigger="click">
                <span class="el-dropdown-link"> 红色光<i class="el-icon-arrow-down el-icon--right"></i> </span>
                <template #dropdown>
                  <el-dropdown-menu>
                    <el-dropdown-item icon="el-icon-plus">红色光</el-dropdown-item>
                    <el-dropdown-item icon="el-icon-circle-plus">蓝色光</el-dropdown-item>
                    <el-dropdown-item icon="el-icon-circle-plus-outline">绿色光</el-dropdown-item>
                  </el-dropdown-menu>
                </template>
              </el-dropdown> -->
              </div>
            </div>

            <div class="params__formItem">
              <div class="params__formLabel">高度角：</div>
              <div class="params__formInput">
                <el-input-number v-model="params.snownum" controls-position="right" :min="0" :max="1000"></el-input-number>
              </div>
              <span class="params__formDu">。</span>
            </div>
            <div class="params__formItem">
              <div class="params__formLabel">方位角：</div>
              <div class="params__formInput">
                <el-input-number v-model="params.cloudnum" controls-position="right" :min="0" :max="1000"></el-input-number>
              </div>
              <span class="params__formDu">。</span>
            </div>
          </div>
        </div>
        <div class="content-item__button">
          <!-- <span class="button"> 取消</span> -->
          <el-button>取消</el-button>
          <el-button type="primary" @click="handleSubmit">确定</el-button>
          <!-- <span class="button"> 确定</span> -->
        </div>
      </div>
      <div v-if="isActive === 3" class="environment-setting__content">
        <div class="content-item">
          <span>时间设置</span>
          <SvgIcon svg-name="close" :size="16" @click="handleClose()"></SvgIcon>
        </div>
        <div class="content-item__detail">
          <div class="params-time__item">
            <div class="params-time__input">
              <el-input-number v-model="params.rainnum" controls-position="right" :min="0" :max="23"></el-input-number>
            </div>
            <span class="params-time__unit">时</span>
          </div>

          <div class="params-time__item">
            <div class="params-time__input">
              <el-input-number v-model="params.snownum" controls-position="right" :min="0" :max="59"></el-input-number>
            </div>
            <span class="params-time__unit">分</span>
          </div>
          <div class="params-time__item">
            <div class="params-time__input">
              <el-input-number v-model="params.cloudnum" controls-position="right" :min="0" :max="59"></el-input-number>
            </div>
            <span class="params-time__unit">秒</span>
          </div>
        </div>

        <div class="content-item__button">
          <!-- <span class="button"> 取消</span> -->
          <el-button>取消</el-button>
          <el-button type="primary" @click="handleSubmit">确定</el-button>
          <!-- <span class="button"> 确定</span> -->
        </div>
      </div>
    </div>
    <div class="temprature-block">
      <div ref="temperature" style="width: 500px; height: 500px; text-align: center"></div>
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts';
import 'echarts-wordcloud';
export default {
  name: 'GreenHouse',
  props: {
    msg: { type: String, default: '' },
  },
  data() {
    return {
      count: 0,
      weatherList: [
        { name: 'sun', text: '晴天' },
        { name: 'cloudy', text: '阴天' },
        { name: 'snowy', text: '雪天' },
        { name: 'foggy', text: '雾天' },
        { name: 'rainy', text: '雨天' },
      ],
      lightingList: [{ name: 'light', text: '自然光' }],

      params: {
        rainnum: 0,
        snownum: 0,
        cloudnum: 0,
        fognum: 0,
      },
      activeIndex: 0,
      isClosed: true,
      isActive: 0,
      lightColor: '',
    };
  },
  mounted() {
    this.drawTemperature();
  },
  methods: {
    handleMetricClicked(item) {
      this.activeIndex = item;
    },
    handleFoldWeather() {
      this.isActive = 1;
      this.isClosed = false;
    },
    handleFoldLighting() {
      this.isActive = 2;

      this.isClosed = false;
    },
    handleFoldTime() {
      this.isActive = 3;

      this.isClosed = false;
    },
    handleClose() {
      this.isClosed = true;
      this.isActive = 0;
    },
    drawTemperature() {
      // this.isOpen = true;

      // var myChart = echarts.init(document.getElementsByClassName('weather'));
      var myChart = echarts.init(this.$refs['temperature']);
      let option = {
        series: [
          {
            type: 'gauge',
            center: ['50%', '60%'],
            startAngle: 200,
            endAngle: -20,
            min: 0,
            max: 60,
            splitNumber: 12,
            itemStyle: {
              color: 'rgba(64, 158, 255, 0.6)',
            },
            progress: {
              show: true,
              width: 30,
            },

            pointer: {
              show: false,
            },
            axisLine: {
              lineStyle: {
                width: 30,
              },
            },
            axisTick: {
              distance: -45,
              splitNumber: 5,
              lineStyle: {
                width: 2,
                color: 'rgba(255, 255, 255, 0.95)',
              },
            },
            splitLine: {
              distance: -52,
              length: 14,
              lineStyle: {
                width: 3,
                color: 'rgba(255, 255, 255, 0.95)',
              },
            },
            axisLabel: {
              distance: -20,
              color: 'rgba(255, 255, 255, 0.95)',
              fontSize: 20,
            },
            anchor: {
              show: false,
            },
            title: {
              show: false,
            },
            detail: {
              valueAnimation: true,
              width: '60%',
              lineHeight: 40,
              height: '15%',
              borderRadius: 8,
              offsetCenter: [0, '-15%'],
              fontSize: 60,
              fontWeight: 'bolder',
              formatter: '{value} °C',
              color: 'auto',
            },
            data: [
              {
                value: 20,
              },
            ],
          },

          {
            type: 'gauge',
            center: ['50%', '60%'],
            startAngle: 200,
            endAngle: -20,
            min: 0,
            max: 60,
            itemStyle: {
              color: 'rgba(64, 158, 255, 0.8)',
            },
            progress: {
              show: true,
              width: 8,
            },

            pointer: {
              show: false,
            },
            axisLine: {
              show: false,
            },
            axisTick: {
              show: false,
            },
            splitLine: {
              show: false,
            },
            axisLabel: {
              show: false,
            },
            detail: {
              show: false,
            },
            data: [
              {
                value: 20,
              },
            ],
          },
        ],
      };

      setInterval(function () {
        let random = (Math.random() * 60).toFixed(2) - 0;
        option.series[0].data[0].value = random;
        option.series[1].data[0].value = random;
        myChart.setOption(option, true);
      }, 2000);
      option && myChart.setOption(option);
    },
    // drawDiagram() {
    //   var $ = go.GraphObject.make;
    //   var myDiagramDiv = $(go.Diagram, 'myDiagramDiv');
    // },
  },
};
</script>
<style lang="scss">
@import 'src/common/css/constant.scss';
.green-house {
  display: flex;
  justify-content: flex-end;
  margin: 40px;
}
.environment {
  position: absolute;
  left: 334px;
  top: 84px;

  // height: 100%;
  background-image: url('./assets/imgs/bg.jpg');
  background-size: cover;

  .bar {
    color: #fff;
    background: #1f1f1f;
    box-shadow: 0 1px 2px -2px rgba(0, 0, 0, 0.64), 0 3px 6px 0 rgba(0, 0, 0, 0.48), 0 5px 12px 4px rgba(0, 0, 0, 0.36);
    border-radius: 8px;
    width: 344px;
    height: 56px;
    bottom: 100px;
    left: 50%;
    transform: translateX(-50%);
  }
  .environment-setting {
    &__header {
      width: 470px;
      height: 36px;
      background: #1f1f1f;
      box-shadow: 0px 12px 48px 16px rgba(0, 0, 0, 0.12), 0px 9px 28px 0px rgba(0, 0, 0, 0.2), 0px 6px 16px -8px rgba(0, 0, 0, 0.32);
      border-radius: 2px;
      display: flex;
      padding: 0 16px;
    }
    &__content {
      margin-top: 4px;
      padding-bottom: 16px;
      width: 470px;
      // height: 288px;
      background: #1f1f1f;
      box-shadow: 0px 12px 48px 16px rgba(0, 0, 0, 0.12), 0px 9px 28px 0px rgba(0, 0, 0, 0.2), 0px 6px 16px -8px rgba(0, 0, 0, 0.32);
    }
  }
  .header-item {
    font-weight: 400;
    color: rgba(255, 255, 255, 0.85);
    line-height: 20px;
    display: flex;
    align-items: center;
    font-size: 14px;
    cursor: pointer;
    &.active {
      color: rgba(23, 125, 220, 1);
      .icon {
        color: rgba(23, 125, 220, 1) !important;
      }
    }
    &__key {
    }
    &__value {
      margin: 0 8px 0 3px;
    }
    .svg-icon {
    }
  }

  .vertical-line {
    margin: auto 16px;
    color: rgba(255, 255, 255, 0.15);
  }
  .content-item {
    height: 46px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.12);
    font-size: 14px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.85);
    display: flex;
    justify-content: space-between;
    line-height: 22px;
    align-items: center;

    margin: 0 16px;
    .icon {
      cursor: pointer;
    }
    &__detail {
      display: flex;
      padding: 16px;
    }
    &__button {
      text-align: center;

      .el-button {
        // margin-left: 8px;
        // width: 65px;
        height: 32px;
        min-width: 60px !important;
        font-size: 14px;
        border: 1px solid rgba(255, 255, 255, 0.2);
      }
    }
  }
  .detail-left {
    border-right: 1px solid rgba(255, 255, 255, 0.12);
    // height: 190px;

    &__item {
      width: 122px;
      height: 40px;
      display: flex;

      font-weight: 400;
      // justify-content: center;
      padding-left: 16px;
      align-items: center;
      color: rgba(255, 255, 255, 0.85);
      // &:hover {
      //   background: rgba(17, 29, 44, 1);

      //   border-right: 2px solid rgba(23, 125, 220, 1);

      // }
      &.active {
        background: #111d2c;
        border-right: 1px solid rgba(23, 125, 220, 1);
        color: rgba(23, 125, 220, 1);
      }
    }
    &__value {
      font-size: 14px;
      font-weight: 400;
      margin-left: 8px;
    }
  }
  .detail-right {
    padding-left: 24px;
    .params {
      display: flex;

      &__form {
        display: flex;
        margin-bottom: 24px;
        padding: 0 20px;

        &Item {
          display: flex;
          align-items: center;
          margin-right: 10px;
          padding-bottom: 8px;
          position: relative;
        }
        &Label {
          display: inline;
          // padding-left: 8px;
          width: 72px;
          font-size: 14px;
          white-space: nowrap;
          text-align: right;
          font-weight: 400;
          color: rgba(255, 255, 255, 0.65);
        }
        &Input {
          .el-select {
            width: 190px;
          }
        }
        &Unit {
          margin-left: 8px;
          color: rgba(255, 255, 255, 0.65);
          font-size: 14px;
        }
        &Du {
          color: rgba(255, 255, 255, 0.65);
          font-size: 14px;
          position: absolute;
          top: -1px;
          left: 258px;
        }
      }
    }
  }
  .params-time {
    &__item {
      display: flex;
      align-items: center;
    }
    &__input {
      .el-input-number {
        width: 118px !important;
      }
    }
    &__unit {
      padding: 0 8px;

      font-size: 14px;
      font-weight: 400;
      color: rgba(255, 255, 255, 0.65);
    }
  }
}

.myDiagramDiv {
  width: 400px;
  height: 150px;
  background-color: #ffff;
}
</style>
