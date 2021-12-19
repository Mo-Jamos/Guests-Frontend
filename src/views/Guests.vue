<template>
  <h1>Welcome to Guests</h1>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-md-4 g-4">
      <div class="col" v-for="guest in guests" :key="guest.id">
        <div class="card h-100">
          <img :src="getAvatar(guest)" class="card-img-top" :alt="guest.firstName + ' ' + guest.lastName">
          <div class="card-body">
            <h5 class="card-title">{{ guest.firstName }} {{ guest.lastName }}</h5>
            <p class="card-text">
              {{ guest.firstName }} {{ guest.lastName }} is {{ guest.invited ? 'invited' : 'not invited' }} to
              the wedding on {{ guest.wday }} .
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Guests',
  data () {
    return {
      guests: []
    }
  },
  methods: {
    getAvatar (guest) {
      if (guest.invited === true) {
        return require('../assets/invited.png')
      } else if (guest.invited === false) {
        return require('../assets/notinvited.png')
      }
    }
  },
  mounted () {
    const endpoint = process.env.VUE_APP_BACKEND_BASE_URL + '/api/v1/guests'
    const requestOptions = {
      method: 'GET',
      redirect: 'follow'
    }

    fetch(endpoint, requestOptions)
      .then(response => response.json())
      .then(result => result.forEach(guest => {
        this.guests.push(guest)
      }))
      .catch(error => console.log('error', error))
  }
}
</script>

<style scoped>

</style>
