<template>
  <div class="mdl-grid">
    <div class="mdl-cell mdl-cell--8-col">
      <div class="picture">
        <img :src="this.pictures[$route.params.id].url" />
      </div>
      <div class="info">
        <span>{{ this.pictures[$route.params.id].info }}</span>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--8-col-tablet">
      <div class="comment">
        <span>{{ this.pictures[$route.params.id].comment }}</span>
      </div>
      <div class="actions">
        <router-link class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" to="/post">
          ANSWER
        </router-link>
      </div>
      <div class="input">
        <form @submit.prevent="post">
          <div class="mdl-textfield mdl-js-textfield">
            <input class="mdl-textfield__input" type="text" id="sample1" ref="sampletext">
          </div>
          <button class="mdl-button mdl-js-button mdl-button--icon mdl-button--colored" type="submit">
            <i class="material-icons">done</i>
          </button>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import data from '../data'
import VueResource from 'vue-resource'
import Vue from 'vue'
Vue.use(VueResource)
export default {
  methods: {
    post () {
      console.log(this.$refs.sampletext.value)
      // var formData = new FormData()
      // formData.append('foo', 'bar')
      var formData = {'foo': 'bar'}
      this.$http.post('http://35.160.134.174/vue', formData).then(response => {
        console.log(response.body)
      }, response => {
        // error callback
      })
    }
  },
  data () {
    return {
      'pictures': data.pictures
    }
  }
}
</script>
<style scoped>
  .picture > img {
    color: #fff;
    width:100%;
  }
  .info {
    text-align: right;
    padding: 5px;
    color: #555;
    font-size: 10px;
  }
  .comment {
    padding: 10px;
    color: #555;
  }
  .actions {
    text-align: center;
  }
</style>
