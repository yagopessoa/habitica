<template lang="pug">
.row.flex-xl-nowrap
  side-menu
    .side-menu-header.d-none.d-sm-block {{ $t('settings') }}
    router-link.nav-link(:to="{name: 'site'}", exact, :class="{'active': $route.name === 'site'}") {{ $t('general') }}
    router-link.nav-link(:to="{name: 'subscription'}", :class="{'active': $route.name === 'subscription'}") {{ $t('subscription') }}
    router-link.nav-link(:to="{name: 'api'}", :class="{'active': $route.name === 'api'}") {{ $t('siteData') }}
    router-link.nav-link(:to="{name: 'notifications'}", :class="{'active': $route.name === 'notifications'}") {{ $t('notifications') }}

  .col-12.col-md-9
    router-view
</template>

<script>
import SideMenu from 'client/components/sideMenu';

export default {
  components: {
    SideMenu,
  },
};
</script>
