<script>
import { RouterView } from "vue-router";
import { mapWritableState, mapActions } from "pinia";
import { useUserStore } from "./stores/user";
export default {
  methods: {
    ...mapActions(useUserStore, ["handleCredentialResponse"]),
  },
  computed: {
    ...mapWritableState(useUserStore, ["isSignin"]),
  },
  components: {
    RouterView,
  },
  created() {
    if (this.statusBar) this.statusBar = "eat";
    if (localStorage.getItem("access_token")) this.isSignin = true;
  },
  mounted() {
    window.onload = async () => {
      // eslint-disable-next-line no-undef
      google.accounts.id.initialize({
        client_id:
          "718039942199-iqptd974osltloc2mavns1ess4vm5ucp.apps.googleusercontent.com",
        callback: this.handleCredentialResponse,
      });
      // eslint-disable-next-line no-undef
      google.accounts.id.renderButton(
        document.getElementById("buttonDiv"),
        { theme: "outline", size: "large" } // customization attributes
      );
      // eslint-disable-next-line no-undef
      google.accounts.id.prompt(); // also display the One Tap dialog
    };
  },
};
</script>

<template>
  <RouterView />
</template>
