<template>
  <div class="footer-background">
    <div class="row">
      <div class="col text-center fa-icons">
        <a :href="$t('links.twitter')" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a>
        <a :href="$t('links.discord')" target="_blank"><i class="fa fa-comments" aria-hidden="true"></i></a>
        <a :href="$t('links.telegram')" target="_blank"><i class="fa fa-telegram" aria-hidden="true"></i></a>
        <a :href="$t('links.medium')" target="_blank"><i class="fa fa-medium" aria-hidden="true"></i></a>
        <a :href="$t('links.github')" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>
      </div>
    </div>
    <div class="row">
      <div class="col text-center copyright-col">
        <a :href="$t('links.contract')" target="_blank">{{ $t("footer.copyRight") }}</a>
      </div>
    </div>
  </div>
</template>

<script>
	export default {
		name: "Footer",
	}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
@import "../styles/colors.scss";
@import "../styles/fonts.scss";

.footer-background {
  color: $fontColor;
  padding: 45px 0 30px;

  .footer-logo {
    height: 32px;
  }
  .footer-col {
    margin: 45px 0;
  }
  .fa-icons {
    margin-bottom: 15px;
  }
  .fa-icons > a {
    font-size: 27px;
    color: $fontColor;
    margin: 20px 20px;
  }
  .copyright-col > a {
    font-size: 16px;
    color: $fontColor;
  }
}
</style>
