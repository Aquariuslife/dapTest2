<template>
  <div class="home-container">
    <div class="wrap" ref="editor">
      <div class="top"></div>

      <sinan />
      <seamless />
      <pyramid />

      <scrollArc />
      <szBar />

      <ringPin />
      <rotateColorful />
      <circleRunway />
      <scanRadius />

      <cakeLinkage />
      <pyramidTrend />
      <dynamicLine />

      <staffMix />
      <flashCloud />
      <ringPie />
      <colorfulRadar />

      <dynamicList />
      <bar3d />
      <colorfulArea />

      <rainbow />
      <gauge />
      <waterPolo />
      <circleNesting />

      <div class="divider"></div>
    </div>
  </div>
</template>

<script>
import { screenSize } from '@/assets/js/utils';
import bgAnimation from '../components/bgAnimation/index.vue'; // 登录界面背景图动画
import modal from '../components/modal/index.vue'; // 自定义全局模态框
import sinan from '../components/sinan/index.vue'; // 司南排名图
import seamless from '../components/seamless/index.vue'; // 新闻无缝滚动
import pyramid from '../components/pyramid/index.vue'; // 金字塔动画
import scrollArc from '../components/scrollArc/index.vue'; // 滚动弧形线
import szBar from '../components/szBar/index.vue'; // 双轴柱状图
import ringPin from '../components/ringPin/index.vue'; // 环形气泡图
import rotateColorful from '../components/rotateColorful/index.vue'; // 旋转多彩图
import circleRunway from '../components/circleRunway/index.vue'; // 环形跑道图
import scanRadius from '../components/scanRadius/index.vue'; // 扫描半径图
import cakeLinkage from '../components/cakeLinkage/index.vue'; // 柱饼组合联动
import dynamicLine from '../components/dynamicLine/index.vue'; // 动态轮播折线图
import pyramidTrend from '../components/pyramidTrend/index.vue'; // 金字塔趋势
import staffMix from '../components/staffMix/index.vue'; // 人员占比
import flashCloud from '../components/flashCloud/index.vue'; // 闪动云
import ringPie from '../components/ringPie/index.vue'; // 环形饼图
import colorfulRadar from '../components/colorfulRadar/index.vue'; // 多彩雷达
import dynamicList from '../components/dynamicList/index.vue'; // 动态列表动画
import bar3d from '../components/bar3d/index.vue'; // 3D立体柱状图
import colorfulArea from '../components/colorfulArea/index.vue'; // 多彩轮播面积
import rainbow from '../components/rainbow/index.vue'; // 彩虹轨道图
import gauge from '../components/gauge/index.vue'; // 仪表盘
import waterPolo from '../components/waterPolo/index.vue'; // 水球图
import circleNesting from '../components/circleNesting/index.vue'; // 圆环套圆环

import business from '../components/companySummary/business.vue'; // 业务范围
import talent from '../components/companySummary/talent.vue'; // 人才队伍
import income from '../components/companySummary/income.vue'; // 营业收入
import wordCloud from '../components/companySummary/wordCloud.vue'; // 产品热词
import distribution from '../components/companySummary/distribution.vue'; // 客户分布
import history from '../components/companySummary/history.vue'; // 发展历程
export default {
  name: 'Home',
  components: {
    bgAnimation,
    modal,
    sinan,
    seamless,
    pyramid,
    scrollArc,
    szBar,
    ringPin,
    rotateColorful,
    circleRunway,
    scanRadius,
    cakeLinkage,
    dynamicLine,
    pyramidTrend,
    staffMix,
    flashCloud,
    ringPie,
    colorfulRadar,
    dynamicList,
    bar3d,
    colorfulArea,
    rainbow,
    gauge,
    waterPolo,
    circleNesting,

    business,
    talent,
    income,
    wordCloud,
    distribution,
    history,
  },
  data() {
    return {};
  },
  computed: {},
  created() {},
  mounted() {
    screenSize(this.$refs.editor);
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
.home-container {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  .wrap {
    transform-origin: 0px 0px 0px;
    background: url(../assets/img/bj.jpg) no-repeat;
    background-size: contain;
    background-position: 50% 0;
    background-color: rgb(0, 0, 0);
    min-width: auto;
    width: 1920px;
    min-height: auto;
    height: 1080px;
    overflow: auto;
    .top {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 80px;
      background-color: transparent;
      background: url(../assets/img/top_nav.png) no-repeat;
      background-position: 65% 0;
      border: none;
      overflow: hidden;
    }
    .divider {
      position: absolute;
      left: 50px;
      top: 3253px;
      width: 90%;
      height: 50px;
      width: 300px;
      border: none;
      background: transparent;
    }
  }
}
</style>
