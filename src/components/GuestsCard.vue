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
              {{ guest.firstName }} {{ guest.lastName }} is {{ guest.invited ? 'invited and coming' : 'not invited or not coming' }} to
              the wedding and they are coming  {{ guest.plusOne ? 'with a plus One' : 'Alone' }} Notes to this Person are: {{guest.note}} Email is {{guest.email}} and the relationship is {{guest.relationship}} .
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

  /* async sendEmail () {
    const nodemailer = require('nodemailer')
    const { google } = require('googleapis')
    const CLIENT_ID = '925851217739-achion3n7hqtnfo1rcu2r7skof7e5s5f.apps.googleusercontent.com'
    const CLIENT_SECRET = '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'
    const REDIRECT_URI = 'https://developers.google.com/oauthplayground'
    const REFRESH_TOKEN = '1//04OcRX6-4T0wwCgYIARAAGAQSNwF-L9IrXJagECJSsrlBdHiDsmd6c4HKwvD4CLtPYtan8hAueaIzgc2xPIWkURfi4rMxrVu0Z14'
    const oAuth2Client = new google.auth.OAuth2(CLIENT_ID, CLIENT_SECRET, REDIRECT_URI)
    oAuth2Client.setCredentials({ refresh_token: REFRESH_TOKEN })
    try {
      const accessToken = await oAuth2Client.getAccessToken()
      const transport = nodemailer.createTransport({
        service: 'gmail',
        auth: {
          type: 'OAuth2',
          user: 'webtechwebtechprojekt@gmail.com',
          clientId: CLIENT_ID,
          clientSecret: CLIENT_SECRET,
          refreshToken: REFRESH_TOKEN,
          accessToken: accessToken
        }
      })
      const mailOptions = {
        from: 'webtechwebtechprojekt@gmail.com <webtechwebtechprojekt@gmail.com>',
        to: 'webtechwebtechprojekt@gmail.com',
        subject: 'Hello from gmail using API',
        text: 'Hello from gmail email using API',
        html: '<h1>Hello from gmail email using API</h1>'
      }
      const result = await transport.sendEmail(mailOptions)
      return result
    } catch (error) {
      return error
    }
  }

}, */
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
