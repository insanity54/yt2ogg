<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
	<h2>Paste the URL of the youtube video below</h2>
	<div>
		<b-form-input v-model="text1"
					  type="text"
					  placeholder="Enter your name"></b-form-input>
		<p>{{ text1 }}</p>
	</div>
  </div>
  

</template>

<script>

//import { YouTubeURLParser } from "@iktakahiro/youtube-url-parser"
//const parser = new YouTubeURLParser("https://youtu.be/7lmCu8wz8ro?t=2m10s")

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Convert YouTube Videos to a sound file',
	  text1: ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
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
