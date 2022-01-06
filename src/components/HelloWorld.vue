<template>
  <h1>{{msg}}</h1>
  <img style="margin-left: 100px; width:500px;" alt='Vue logo' src='../assets/schriftzug.png'>
  <div class="hello">
    <div
      style='
        margin: 0 auto;
        width:300px;
        padding: 16px 0 16px 0;
        border: 1px solid black;
        background-color: magenta;
      '
    >
      <form
        action='SENDEADRESSE'
        id='ft-form'
        method='POST'
        accept-charset='UTF-8'
      >
        <h1 style="color:white">Testüberschrift</h1>
        <h6 style="color:white">Unterüberschrift</h6>
        <input placeholder="Vorname" type='text' name='Name' required /><br><br>
        <input placeholder="Nachname" type='text' name='E-Mail' required /><br><br>
        <input placeholder="E-Mail-Adresse" type='email' name='E-Mail' required /><br><br>
        <input placeholder="Telefon" type="tel" name='Telefon' required /><br><br>
        <textarea rows='4' placeholder="Geben Sie hier Ihre Nachricht ein..." name='Nachricht' required></textarea>
        <div class='btns'>
          <input type='submit' value='Absenden' />
        </div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
