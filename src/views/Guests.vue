<template>
  <div class="guests">
    <GuestsCard msg=""/>
  </div>
</template>

<script>
// @ is an alias to /src
import GuestsCard from '@/components/GuestsCard.vue'

export default {
  name: 'Guests',
  components: {
    GuestsCard
  }
}
</script>
