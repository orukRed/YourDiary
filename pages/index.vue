<template>

</template>

<script>
// import Logo from '~/components/Logo.vue'
// import VuetifyLogo from '~/components/VuetifyLogo.vue'
import Vue from 'Vue'
export default Vue.extend({
  layout:'MenuBar',
  fetch({ redirect }) {
    redirect(301, '/View');//リダイレクト
  }

})

</script>
