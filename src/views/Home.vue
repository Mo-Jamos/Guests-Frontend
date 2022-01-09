<template>
  <div class="home">
   <!-- <img alt="Vue logo" src="../assets/logo.png">-->
    <GuestsCreateForm msg=""/>
    <Time msg=""/>
  </div>
</template>

<script>
// @ is an alias to /src
import GuestsCreateForm from '@/components/GuestsCreateForm.vue'
import Time from '@/components/Time.vue'

export default {
  name: 'Home',
  components: {
    GuestsCreateForm,
    Time
  }
}
</script>
