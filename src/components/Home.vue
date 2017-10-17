<template>
  <div class="hello">
    <h1>
      <router-link to="/funnel">{{ h1 }}</router-link>
    </h1>
    <form v-on:submit.prevent="onSubmit">
      <input placeholder="type" type="text" name="type" ref="my_input">
       <input placeholder="price" type="text" name="price" ref="my_input2">
      <input type="submit" @click.prevent="getFormValues()" name="" value="Submit">
    </form>
  </div>
</template>
<script>
// import axios from 'axios'
/* eslint-disable */
var apigClientFactory = require('aws-api-gateway-client').default

var apigClient = apigClientFactory.newClient({
  region: 'us-east-2',
  invokeUrl: 'https://v2wh86rpe4.execute-api.us-east-2.amazonaws.com'
})

var pathTemplate = '/test/pets'
var method = 'GET'
var additionalParams = {
  headers: { },
  queryParams: { },
 
}



export default {
  name: 'home',
  data () {
    return {
    
      h1: 'Hi there! Ready to relax?'
    }
  },
  methods: {
    getFormValues (){
      const type = document.querySelector("input[name=type]").value
      const price = document.querySelector("input[name=price]").value

      var body={
     'type':type,
    "price": parseFloat(price)
  }
 
      apigClient.invokeApi({}, pathTemplate, method, additionalParams, body, {})
    .then(function (result) {
        // Return the response data
      console.log(JSON.stringify(result.data))
    }).catch(function (result) {

    })
    }
    }

  }

/* eslint-enable */
</script>

<!-- Add "scoped" attribute to limit CSS to this component only
      axios.post('https://0pu2ms8ymi.execute-api.us-east-2.amazonaws.com/test/pets', {
        'type': 'dog',
        'price': 2492.99
      })
        .then(function(response) {
          console.log(response.data)
        })
        .catch(function(error) {
          console.log(error)
        })
 -->
<style scoped>
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