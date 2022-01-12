<template>
  <img style="margin-right: 1800px; width:150px;" src='../assets/schriftzug.png'>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-md-4 g-4">
      <div class="col" v-for="guest in guests" :key="guest.id">
        <div class="card h-100">
          <img :src="getAvatar(guest)" class="card-img-top" :alt="guest.firstName + ' ' + guest.lastName">
          <div class="card-body">
            <h5 class="card-title">{{ guest.firstName }} {{ guest.lastName }}</h5>
            <p class="card-text">
              {{ guest.firstName }} {{ guest.lastName }} with the following Email { {{guest.email}} } is {{ guest.invited ? 'invited and coming' : 'not invited or not coming' }} to
              the wedding and they are coming  {{ guest.plusOne ? 'with a plus One' : 'Alone' }} Extra Notes to this Person { {{guest.note}} } and the relationship is {{guest.relationship}} .
            </p>
            <button type="submit" class="btn btn-primary me-7" @click.prevent="deleteGuest(guest)" style="background-color: red; border: black">Delete</button>
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
    },
    deleteGuest (guest) {
      const endpoint = process.env.VUE_APP_BACKEND_BASE_URL + '/api/v1/guests/' + guest.id
      const requestOptions = {
        method: 'DELETE',
        redirect: 'follow'
      }

      fetch(endpoint, requestOptions)
        .then(response => response.text())
        .then(result => console.log(result))
        .catch(error => console.log('error', error))
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
