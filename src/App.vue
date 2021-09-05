<template>
  <div class="body">
    <div class="main">
      <!-- PRINCIPAL TITLE -->
      <h1 class="title">Text to Speech 🔊</h1>
      <hr />
      <!-- END PRINCIPAL TITLE -->
      <!-- TEXT-TO-SPEECH -->
      <div class="form">
        <form @submit.prevent="getSpeech">
          <select class="languages" v-model="options.language">
            <option value="" hidden>--- Select language ---</option>
            <option v-for="(item, index) of languages" :key="index" :value="item.value">
              {{ item.language }}
            </option>
          </select>
          <textarea name="src" cols="30" rows="10" v-model.trim="options.text"></textarea>
          <button type="submit">Listen<i class="fas fa-volume-up" :style="{'margin-left': '5px'}"></i></button>
          <button @click="options.text = ''">Clear<i class="fas fa-trash" :style="{'margin-left': '5px'}"></i></button>
        </form>
        <audio :src="src" controls autoplay controlslist="nodownload"></audio>
      </div>
      <!-- END TEXT-TO-SPEECH -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      options: {
        url_base: 'http://api.voicerss.org/',
        api_key: '17f3fc8c173b41f3920eb2aed76ca325',
        text: '',
        language: '',
      },
      src: '',
      languages: [
        {
          language: 'English',
          value: 'en-us'
        },
        {
          language: 'French',
          value: 'fr-fr'
        },
        {
          language: 'Italian',
          value: 'it-it'
        },
        {
          language: 'Portuguese',
          value: 'pt-pt'
        },
        {
          language: 'Spanish',
          value: 'es-mx'
        }
      ]
    }
  },
  methods: {
    getSpeech () {
      // Default value for language
      if (!this.options.language) {
        this.options.language = 'en-us'
      }
      if (this.options.text) {
        this.src = `${this.options.url_base}?key=${this.options.api_key}&hl=${this.options.language}&src=${this.options.text}`
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;700&display=swap');

*
{
  margin: 0;
  padding: 0;
}

*, 
*::after, 
*::before
{
  box-sizing: border-box;
}

:root
{
  --dark: #313131;
  --white: #FFF;
  --darkText: #3d3d3d;
  --darkBody: #464646;
}

body
{
  background-color: var(--darkBody);
}

.body
{
  font-family: 'Source Sans Pro', sans-serif;
}

.title
{
  letter-spacing: 0.5px;
  font-weight: 400;
}

.main
{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 50%;
  padding: 24px;
  color: var(--white)
}

@media only screen and (max-width: 600px) {
  .main {
    width: 100%;
  }
}

.form
{
  margin-top: 12px;
}

.languages
{
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  text-align: center;
  border: none;
  outline: none;
  background-color: #229395;
  color: var(--white);
  border-radius: 12px;
}

.languages option
{
  font-weight: 700;
  padding: 10px;
}

.languages option:nth-child(odd)
{
  background-color: #7ACBCD;
  color: var(--dark)
}

.form textarea
{
  display: block;
  border: 2px solid #FFF;
  outline: none;
  width: 100%;
  resize: none;
  background-color: var(--darkText);
  color: var(--white);
  padding: 12px;
  font-size: 1.25em;
  font-weight: 600;
  letter-spacing: 1.25px;
  margin-bottom: 10px;
  border-radius: 24px 0 24px 0;
}

.form button
{
  display: inline;
  padding: 16px;
  width: 50%;
  border: none;
  outline: none;
  margin-bottom: 10px;
  border-radius: 0 48px 0 16px;
  background-color: #7ACBCD;
  color: var(--dark);
  font-weight: 800;
  transition: .4s;
  cursor: pointer;
  letter-spacing: 1.5px;
}

.form button:nth-child(4)
{
  border-radius: 48px 0 16px 0;
}

.form button:hover
{
  background-color: #229395;
  color: var(--white);
}

.form audio
{
  width: 100%;
  border: none;
  outline: none;
}
</style>
