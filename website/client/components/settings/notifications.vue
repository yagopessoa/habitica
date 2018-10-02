<template lang="pug">
.row.standard-page
  .col-12
    h1 {{ $t('notifications') }}
  .col-8
    table.table.notifications-table
      tr
        th
          span.title {{ $t('email') }}
        th
          span {{ $t('enabled') }}
      tr
        td
          span {{ $t('receiveEmailNotifications') }}
        td.check-cell
          input(type='checkbox', v-model='user.preferences.emailNotifications.unsubscribeFromAll',
          @change='set("emailNotifications", "unsubscribeFromAll")')
      tr(v-for='notification in notificationsIds')
        td
          span {{ $t(notification) }}
        td.check-cell
          input(type='checkbox', v-model='user.preferences.emailNotifications[notification]',
            @change='set("emailNotifications", notification)')

    h2 {{ $t('mobile') }}
    span {{ $t('mobileNotificationsSubscription') }}


</template>

<style lang="scss" scoped>
  @import '~client/assets/scss/colors.scss';

  .notifications-table {
    td {
      padding-top:16px;
      padding-bottom: 16px;
      vertical-align: middle;
    }

    span {
      font-size: 16px;
      font-weight: bold;
      font-stretch: condensed;
      line-height: 1.25;
    }

    .title {
      font-size: 20px;
    }

    .check-cell {
      text-align: center;
    }
  }

</style>

<script>
import { mapState } from 'client/libs/store';
import notificationsMixin from 'client/mixins/notifications';

export default {
  mixins: [notificationsMixin],
  data () {
    return {
      notificationsIds: [
        'newPM',
        'wonChallenge',
        'giftedGems',
        'giftedSubscription',
        'invitedParty',
        'invitedGuild',
        'kickedGroup',
        'questStarted',
        'invitedQuest',
        'importantAnnouncements',
        'weeklyRecaps',
        'onboarding',
      ],
    };
  },
  computed: {
    ...mapState({user: 'user.data'}),
  },
  async mounted () {
    // If ?unsubFrom param is passed with valid email type,
    // automatically unsubscribe users from that email and
    // show an alert

    // A simple object to map the key stored in the db (user.preferences.emailNotification[key])
    // to its string id but ONLY when the preferences' key and the string key don't match
    const MAP_PREF_TO_EMAIL_STRING = {
      importantAnnouncements: 'inactivityEmails',
    };

    const unsubFrom = this.$route.query.unsubFrom;

    if (unsubFrom) {
      await this.$store.dispatch('user:set', {
        [`preferences.emailNotifications.${unsubFrom}`]: false,
      });

      const emailTypeString = this.$t(MAP_PREF_TO_EMAIL_STRING[unsubFrom] || unsubFrom);
      this.text(this.$t('correctlyUnsubscribedEmailType', {emailType: emailTypeString}));
    }
  },
  methods: {
    set (preferenceType, notification) {
      let settings = {};
      settings[`preferences.${preferenceType}.${notification}`] = this.user.preferences[preferenceType][notification];
      this.$store.dispatch('user:set', settings);
    },
  },
};
</script>
