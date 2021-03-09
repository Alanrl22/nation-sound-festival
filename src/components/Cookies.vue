<template>
  <vue-cookie-accept-decline
    :ref="'myPanel1'"
    :elementId="'myPanel1'"
    :debug="false"
    :position="'bottom-left'"
    :type="'floating'"
    :disableDecline="false"
    :transitionName="'slideFromBottom'"
    :showPostponeButton="false"
    @status="cookieStatus"
    @clicked-accept="cookieClickedAccept"
    @clicked-decline="cookieClickedDecline"
  >
    <!-- Optional -->
    <div slot="postponeContent">
      &times;
    </div>

    <!-- Optional -->
    <div slot="message">
      Nous utilisons des cookes pour améliorer votre expérience sur notre site.
      <a href="https://cookiesandyou.com/" target="_blank">Lire plus...</a>
    </div>

    <!-- Optional -->
    <div slot="declineContent">
      Refuser
    </div>

    <!-- Optional -->
    <div slot="acceptContent">
      Accepter
    </div>
  </vue-cookie-accept-decline>
</template>

<script>
// <!-- css import for when you're importing the css directly in your js  -->
import "vue-cookie-accept-decline/dist/vue-cookie-accept-decline.css";

import VueCookieAcceptDecline from "vue-cookie-accept-decline";
// Vue.component('vue-cookie-accept-decline', VueCookieAcceptDecline)

export default {
  components: {
    VueCookieAcceptDecline,
  },
  data() {
    return {
      status,
    };
  },
  methods: {
    cookieStatus: function() {
      console.log("Status en attente");
      this.status = "waiting";
    },
    cookieClickedAccept: function() {
      console.log("L'utilisateur accepte !");
      this.status = "accepted";
    },
    cookieClickedDecline: function() {
      console.log("L'utilisateur refuse :/");
      this.status = "declined";
    },
  },
};
</script>

<style lang="scss">
.cookie {
  background: white;
  border: 1px solid black;
  border-radius: 0;
  box-shadow: -4px 5px 0px 0px #ff8e4e;

  // Floating style
  &__floating {
    a {
      color: #668cb5;
      font-weight: bold;
    }

    &__buttons {
      border-top: 1px solid black;
      font-weight: bold;

      &__button {
        color: black;

        &:first-child {
          border-right: 1px solid black;
        }
        &--accept {
          background: var(--green);

          &:hover {
            background: #8dce9c;
          }
        }
        &--decline {
          background: var(--blue);

          &:hover {
            background: #6292c5;
          }
        }
      }
    }
  }
}
</style>
