<template>
  <div class="container is-max-desktop">
    <article class="tile is-child box">
      <p class="subtitle">URL EXPANDER 🔎</p>
      <b-field grouped>
        <b-input v-model="shortUrl"  placeholder="Type short url here.." expanded></b-input>
        <p class="control">
          <button :disabled="control" class="button is-primary" @click="postUrl">Expand</button>
        </p>
      </b-field>
      <b-notification  ref="element"  :closable="false">
        <b-field>
          <b-input  type="textarea" readonly="true" v-model="result"/>
        </b-field>
        <b-loading :is-full-page="false" :active.sync="isLoading" :can-cancel="false"></b-loading>
      </b-notification>
    </article>
  </div>
</template>

<script>
  import axios from "axios";
  const apiUrl = "https://url-expander-api.herokuapp.com/api/v1/shortlink"
  export default {
    name: 'Search',
    data() {
      return {
        result: "Type a short url and click expand button.",
        shortUrl: "",
        isLoading: false,
      };

    },
    computed:{
      control() {
        return !/^(?:(?:(?:https?|ftp):)?\/\/)(?:\S+(?::\S*)?@)?(?:(?!(?:10|127)(?:\.\d{1,3}){3})(?!(?:169\.254|192\.168)(?:\.\d{1,3}){2})(?!172\.(?:1[6-9]|2\d|3[0-1])(?:\.\d{1,3}){2})(?:[1-9]\d?|1\d\d|2[01]\d|22[0-3])(?:\.(?:1?\d{1,2}|2[0-4]\d|25[0-5])){2}(?:\.(?:[1-9]\d?|1\d\d|2[0-4]\d|25[0-4]))|(?:(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)(?:\.(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)*(?:\.(?:[a-z\u00a1-\uffff]{2,})))(?::\d{2,5})?(?:[/?#]\S*)?$/i.test(this.shortUrl);
      }
    },
    methods: {
      async postUrl() {
        try {
          this.isLoading = true
          const response = await axios.post(apiUrl,{
            shortUrl: this.shortUrl,
          });
          this.isLoading = false
          this.result = response.data.webUrl;
        } catch (error) {
          this.isLoading = false
          this.result = "Error!"
        }
      },

    }
  }
</script>

