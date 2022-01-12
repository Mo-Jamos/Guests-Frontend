<template>
  <div class="guests">
    <GuestsCard msg=""/>
    <GuestsCreateFormSidePanel msg=""/>
  </div>
</template>

<script>
// @ is an alias to /src
import GuestsCreateFormSidePanel from '@/components/GuestsCreateFormSidePanel'
import GuestsCard from '@/components/GuestsCard.vue'

export default {
  name: 'Guests',
  components: {
    GuestsCard, GuestsCreateFormSidePanel
  }
}
</script>
