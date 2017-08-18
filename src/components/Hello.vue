<template>
  <div class='hello'>
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <!-- <p>{{pot}}</p> -->
    <div v-for="post in pot">
      <!-- <p>{{post.data}}</p> -->
      <h2 v-for="title in post.data.title">{{title.text}}</h2>
      <p v-for="content in post.data.content">{{content.text}}</p>
    </div>
    <ul>
      <li><a href='https://vuejs.org' target='_blank'>Core Docs</a></li>
      <li><a href='https://forum.vuejs.org' target='_blank'>Forum</a></li>
      <li><a href='https://gitter.im/vuejs/vue' target='_blank'>Gitter Chat</a></li>
      <li><a href='https://twitter.com/vuejs' target='_blank'>Twitter</a></li>
      <br>
      <li><a href='http://vuejs-templates.github.io/webpack/' target='_blank'>Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href='http://router.vuejs.org/' target='_blank'>vue-router</a></li>
      <li><a href='http://vuex.vuejs.org/' target='_blank'>vuex</a></li>
      <li><a href='http://vue-loader.vuejs.org/' target='_blank'>vue-loader</a></li>
      <li><a href='https://github.com/vuejs/awesome-vue' target='_blank'>awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      pot: ''
    }
  },
  methods: {
    getContent () {
      var req
      var Prismic = require('prismic-javascript')
      var apiEndpoint = 'https://gweit.prismic.io/api/v2'
      Prismic.getApi(apiEndpoint, { req: req }).then(function (api) {
        return api.query('') // An empty query will return all the documents
      }).then((response) => {
        console.log('Documents: ', response.results)
        this.pot = response.results
        console.log(response.results)
      }, function (err) {
        console.log('Something went wrong: ', err)
      })
    }
  },
  beforeMount () {
    this.getContent()
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
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
