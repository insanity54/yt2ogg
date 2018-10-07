<template>
<div class="container">
  <h1>{{ msg }}</h1>
  <h2>Paste the URL of the youtube video below</h2>
  <div>
    <b-form-input v-model="text1" type="text" placeholder="Example: https://www.youtube.com/watch?v=il4cAeVzZwI">
    </b-form-input>
    <b-progress class="progressBar" :class="{ invis: progressBarIsInvisible }" :value="100" :max="100" animated></b-progress>
    <b-alert variant="danger"
      dismissible
      :show="showDismissibleAlert"
      @dismissed="showDismissibleAlert=false">
      {{ errorMessage }}
    </b-alert>
    <b-button @click="submitUrl()" size="large" variant="primary">
      Submit
    </b-button>
  </div>
</div>
</template>

<script>
// import { YouTubeURLParser } from "@iktakahiro/youtube-url-parser"
// const parser = new YouTubeURLParser("https://youtu.be/7lmCu8wz8ro?t=2m10s")
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Convert YouTube videos 2 a sound file',
      text1: '',
      progressBarIsInvisible: true,
      showDismissibleAlert: false,
      errorMessage: 'n/a'
    }
  },
  methods: {
    submitUrl: function () {
      var that = this
      console.log(this.text1)
      console.log(window.location.href)
      console.log(window)
      var full = location.protocol + '//' + location.hostname + ':10010'
      console.log(full)

      // start spinner/progress bar and hide any old errors
      that.progressBarIsInvisible = false
      that.showDismissibleAlert = false


      axios({
        url: `${full}/oggme?url=${this.text1}`,
        method: 'GET',
        responseType: 'blob'
      }).then(function (response) {
        // put the spinner on the submit button back to normal
        that.progressBarIsInvisible = true

        console.log(response)
        const url = window.URL.createObjectURL(new Blob([response.data]))
        const link = document.createElement('a')
        link.href = url
        link.setAttribute('download', 'yt2.ogg')
        document.body.appendChild(link)
        link.click()

        // clear input field
        that.text1 = ''
      })
        .catch(function (error) {
          console.log(`on noe there has ben an error=${error}`)
          console.log(error)
          that.progressBarIsInvisible = true
          that.showDismissibleAlert = true
          that.errorMessage = error.message
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@-webkit-keyframes fado {
  0% {
    opacity: 0;
    transform: scale(1, 0);
  }

  100% {
    opacity: 1;
    transform: scale(1, 1);
  }
}

@-moz-keyframes fado {
  0% {
    opacity: 0;
    transform: scale(1, 0);
  }

  100% {
    opacity: 1;
    transform: scale(1, 1);
  }
}

@keyframes fado {
  0% {
    opacity: 0;
    transform: scale(1, 0);
  }

  100% {
    opacity: 1;
    transform: scale(1, 1);
  }
}

.progressBar {
  animation: fado 2s;
}

.invis {
  display: none;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
