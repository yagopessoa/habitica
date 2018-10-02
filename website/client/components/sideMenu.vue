<template lang="pug">
  nav.nav.flex-md-column.col-12.col-md-3.col-xl-2.side-menu
    slot
</template>

<style lang="scss" scoped>
  @import '~client/assets/scss/colors.scss';

  .side-menu {
    background: $gray-600;
    box-shadow: 0 1px 2px 0 rgba($black, 0.2);
    z-index: 9;
    padding-right: 0;
    padding-top: 16px;
  }

  .side-menu-header {
    font-size: 20px;
    font-weight: bold;
    font-family: 'Roboto Condensed', sans-serif;
    line-height: 1.2;
    color: $gray-10;
    padding: 16px 24px;
  }

  .nav-link {
    font-size: 16px;
    padding: 16px 24px;
    font-family: 'Roboto Condensed', sans-serif;
    color: $gray-50;

    &.active {
      color: white;
      font-weight: bold;
      background: $purple-100;
    }

    &:hover {
      background: $gray-500;
      color: $gray-50;
    }
  }
</style>
