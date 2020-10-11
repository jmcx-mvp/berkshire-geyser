<template>
  <div class="dashboard-container">
    <div class="row">
      <div class="col text-center">
        <img class="home-logo" :src="'/static/logo/logo.png'" alt=""/>
      </div>
    </div>
    <div class="row">
      <div class="col text-center welcome-tit">{{ $t("common.welcome") }}</div>
    </div>
    <div class="row">
      <div class="col text-center welcome-txt">{{ $t("common.welcomeTxt") }}</div>
    </div>

    <div class="row">
      <div class="col-xl-4 col-lg-4 col-md-4 col-sm-12 col-xs-12 text-center"
           v-for="(product, index) in products" :key="index">
        <product :product-data="product" :product-index="LPTokenToPoolID(product.LPToken)"></product>
      </div>
    </div>

    <loading :active.sync="loading"
             :can-cancel="false"
             :is-full-page="true"></loading>
  </div>
</template>

<script>
import {LPTokenToPoolID} from "@/utils/web3/constant";
import Product from "./Product";
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';

export default {
  name: "dashboard",
  components: {Product, Loading},

  data() {
    return {
      allBalance: null,
      poolInfo: null,
      loading: false,

      products: [
        {
          img: "/static/icon/UNI-ETH.png",
          name: "UNISWAP",
          txt: "Deposit UNI-ETH UNI-V2 LP Earn BFT",
          tx: "UNI-ETH",
          apy: "1666",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "",
        },
        {
          img: "/static/icon/BFT-ETH.png",
          name: "Berkshire Finance",
          txt: "Deposit BFT-ETH UNI-V2 LP Earn BFT",
          tx: "BFT-ETH",
          apy: "1666",
          stat: true,
          dateTime: "",
          double: true,
          LPToken: "",
        },
        {
          img: "/static/icon/BFT-XMX.png",
          name: "Berkshire XMX",
          txt: "Deposit BFT-XMX UNI-V2 LP Earn BFT",
          tx: "BFT-XMX",
          apy: "1666",
          stat: true,
          dateTime: "",
          double: true,
          LPToken: "",
        },
        {
          img: "/static/icon/$AAPL-ETH.png",
          name: "FruitTech $AAPL",
          txt: "Deposit $AAPL-ETH UNI-V2 LP Earn BFT",
          tx: "$AAPL-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0x5d0a98c2252f3e1ae4ec2320faee5a208bce33fd",
        },
        {
          img: "/static/icon/USDT-ETH.png",
          name: "Microbox USDT",
          txt: "Deposit USDT-ETH UNI-V2 LP Earn BFT",
          tx: "USDT-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          poolIdx: 0,
          LPToken: "0x0d4a11d5eeaac28ec3f61d100daf4d40471f1852",
        },
        {
          img: "/static/icon/sUSD-ETH.png",
          name: "Rainforest sUSD",
          txt: "Deposit sUSD-ETH UNI-V2 LP Earn BFT",
          tx: "sUSD-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0xf80758ab42c3b07da84053fd88804bcb6baa4b5c",
        },
        {
          img: "/static/icon/LEND-ETH.png",
          name: "Good Group LEND",
          txt: "Deposit LEND-ETH UNI-V2 LP Earn BFT",
          tx: "LEND-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0xab3f9bf1d81ddb224a2014e98b238638824bcf20",
        },
        {
          img: "/static/icon/COMP-ETH.png",
          name: "Alimama COMP",
          txt: "Deposit COMP-ETH UNI-V2 LP Earn BFT",
          tx: "COMP-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0xcffdded873554f362ac02f8fb1f02e5ada10516f",
        },
        {
          img: "/static/icon/YFII-ETH.png",
          name: "Elevencent YFII",
          txt: "Deposit YFII-ETH UNI-V2 LP Earn BFT",
          tx: "YFII-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0x8973Be4402bf0a39448f419c2D64bD3591Dd2299",
        },
        {
          img: "/static/icon/DAI-ETH.png",
          name: "Walstore DAI",
          txt: "Deposit DAI-ETH UNI-V2 LP Earn BFT",
          tx: "DAI-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0xa478c2975ab1ea89e8196811f51a7b7ade33eb11",
        },
        {
          img: "/static/icon/BET-ETH.png",
          name: "VIZA BET",
          txt: "Deposit BET-ETH UNI-V2 LP Earn BFT",
          tx: "BET-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0x15e66a9868572e026e122726807ba26e4cf251dc",
        },
        {
          img: "/static/icon/XMX-ETH.png",
          name: "YAMAWA XMX",
          txt: "Deposit XMX-ETH UNI-V2 LP Earn BFT",
          tx: "XMX-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0x46dcb97e7c485ba9d541008e3750803769ad620a",
        },
        {
          img: "/static/icon/RenBTC-ETH.png",
          name: "SAM renBTC",
          txt: "Deposit RenBTC-ETH UNI-V2 LP Earn BFT",
          tx: "RenBTC-ETH",
          apy: "888",
          stat: true,
          dateTime: "",
          double: false,
          LPToken: "0x81fbef4704776cc5bba0a5df3a90056d2c6900b3",
        },
      ]
    }
  },

  methods: {
    LPTokenToPoolID: LPTokenToPoolID,
    seeTheMenu() {
      this.$router.push({name: "Dashboard"})
    },
  },
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
@import "../../styles/colors.scss";
@import "../../styles/fonts.scss";

.dashboard-container {
  width: 100%;
  height: 100%;

  .home-logo{
    width: 120px;
    height: 120px;
  }

  .welcome-tit {
    font-size: 27px;
    color: $fontColor;
    letter-spacing: 2px;
    font-family: $fontTit;
  }
  .welcome-txt {
    margin-bottom: 30px !important;
    color: $txtColor;
    font-family: $fontTxt;
  }
}
</style>
