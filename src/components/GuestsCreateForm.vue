<template>
  <img style="margin-left: 0px; width:500px;" src='../assets/schriftzug.png'>
  <div class="test">
    <form class="row g-3 needs-validation" id="guests-create-form" novalidate>
  <div
    style='
        margin: 0 auto;
        width:400px;
        padding: 50px 0 16px 0;
        background-color: white;
      '
  >

    <h1 style="color:black">Guest information</h1>
    <!-- firstname input -->
    <div class="input-group mb-3" >
      <span class="input-group-text" id="firstname">First name</span>
      <input type="text" class="form-control" placeholder="first name" aria-label="Username" aria-describedby="basic-addon1" v-model="firstName" required>
      <div class="invalid-feedback">
        Please provide a first name.
      </div>
    </div>
    <!-- lastname input -->
    <div class="input-group mb-3">
      <span class="input-group-text" id="lastname">Last name</span>
      <input type="text" class="form-control" placeholder="last name" aria-label="Username" aria-describedby="basic-addon1" v-model="lastName" required>
      <div class="invalid-feedback">
        Please provide a last name.
      </div>
    </div>
    <!-- Email input -->
    <div class="input-group mb-3">
      <input type="text" class="form-control" placeholder="E-mail" aria-label="Recipient's username" aria-describedby="basic-addon2" v-model="email" required>
      <div class="invalid-feedback">
        Please provide an Email.
      </div>
      <span class="input-group-text" id="basic-addon2">@example.com</span>
    </div>
    <!--Notes input-->
    <div class="input-group">
      <span class="input-group-text">Note</span>
      <textarea class="form-control" aria-label="With textarea" v-model="note" required></textarea>
    </div>
    <p></p>
    <!-- Guest is coming or not menu -->
    <div class="input-group mb-3">
      <span class="input-group-text" for="attending">attending...?</span>
      <select id="attending" class="form-select" v-model="invited" required>
        <option value="" selected disabled>Choose... </option>
        <option value="true">Planning on coming</option>
        <option value="false">not coming</option>
      </select>
      <div class="invalid-feedback">
        Please select.
      </div>
    </div>
    <!-- Guest relationship -->
    <div class="input-group mb-3">
      <span class="input-group-text" for="relationShip">Relationship</span>
      <select id="relationShip" class="form-select" v-model="relationship" required>
        <option value="" selected disabled>Choose... </option>
        <option value="brideFamily">bride's Family</option>
        <option value="groomFamily">groom's Family</option>
        <option value="brideFriends">bride Friends</option>
        <option value="groomFriends">groom Friends</option>
        <option value="notRelated">not Related</option>
      </select>
      <div class="invalid-feedback">
        Please select.
      </div>
    </div>
    <!-- plus 1 check box -->
    <div class="mb-3">
      <div class="form-check">
        <input class="form-check-input" type="checkbox" id="FieldsetCheck" v-model="plusOne" required>
        <label class="form-check-label" for="FieldsetCheck" style="margin-right: 300px; color: black">
          check this
        </label>
      </div>
    </div>
    <!-- server Validation Messages -->
    <div v-if="this.serverValidationMessages">
      <ul>
        <li v-for="(message, index) in serverValidationMessages" :key="index" style="color: red">
          {{ message }}
        </li>
      </ul>
    </div>
    <button type="submit" class="btn btn-primary me-3" @click="createGuest">Submit</button>
  </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'GuestsCreateForm',
  data () {
    return {
      firstName: '',
      lastName: '',
      invited: '',
      email: '',
      plusOne: false,
      note: '',
      relationship: '',
      serverValidationMessages: []
    }
  },
  methods: {
    emits: ['created'],
    async createGuest () {
      if (this.validate()) {
        const endpoint = process.env.VUE_APP_BACKEND_BASE_URL + '/api/v1/guests'
        const headers = new Headers()
        headers.append('Content-Type', 'application/json')

        const payload = JSON.stringify({
          firstName: this.firstName,
          lastName: this.lastName,
          invited: this.invited,
          email: this.email,
          plusOne: this.plusOne,
          note: this.note,
          relationship: this.relationship
        })
        const requestOptions = {
          method: 'POST',
          headers: headers,
          body: payload,
          redirect: 'follow'
        }
        const response = await fetch(endpoint, requestOptions)
        await this.handleResponse(response)
      }
    },
    async handleResponse (response) {
      if (response.ok) {
        this.$emit('created', response.headers.get('location'))
        document.getElementById('close-offcanvas').click()
      } else if (response.status === 400) {
        response = await response.json()
        response.errors.forEach(error => {
          this.serverValidationMessages.push(error.defaultMessage)
        })
      } else {
        this.serverValidationMessages.push('Unknown error occurred')
      }
    },
    validate () {
      const form = document.getElementById('guests-create-form')
      form.classList.add('was-validated')
      return form.checkValidity()
    }
  }
}
</script>

<style scoped>

</style>
