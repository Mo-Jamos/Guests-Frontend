<template>
  <div class="about">
    <h1 style="text-align: center;">About<img src="https://html5-editor.net/tinymce/plugins/emoticons/img/smiley-cool.gif" alt="cool" /></h1>
    <p style="text-align: center;">&nbsp;</p>
    <p style="text-align: center;">&nbsp;</p>
    <h1 dir="auto" style="text-align: center;">Save the Date WebTech Projekt</h1>
    <p style="text-align: center;">&nbsp;</p>
    <h2 style="text-align: center;">Eine kleine Webseite zum Verfolgen von Hochzeitsg&auml;sten!</h2>
    <img src="../assets/htw.png" height="300" width="600"/>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p style="text-align: center;">Link zum&nbsp;FrontEnd Repo:&nbsp;<a href="https://github.com/Mo-Jamos/Guests-Frontend">https://github.com/Mo-Jamos/Guests-Frontend</a></p>
    <p style="text-align: center;">Link zum BackEnd Repo: <a href="https://github.com/Mo-Jamos/Save_the_Date_WebTech-Projekt">https://github.com/Mo-Jamos/Save_the_Date_WebTech-Projekt</a></p>
  </div>
  <Time msg=""/>
</template>
<script>
// @ is an alias to /src
import Time from '@/components/Time.vue'

export default {
  name: 'About',
  components: {
    Time
  }
}
</script>
