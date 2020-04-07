<template>
  <ul :class="containerClass">
    <slot
      name="loading"
      :loading="loading"
    />
    <slot
      v-for="(feed, index) in feeds"
      name="feeds"
      :index="index"
      :feed="feed"
    />
    <slot
      name="error"
      :error="error"
    />
  </ul>
</template>

<script>
import axios from 'axios'

export default {
  name: 'VueInstagram',

  props: {
    /*
    * Instagram access token.
    */
    token: {
      type: String,
      required: true
    },

    /*
     * Media Fields (see https://developers.facebook.com/docs/instagram-basic-display-api/reference/media#fields)
     */

    fields: {
      type: [String, Array],
      required: true
    },


    /*
    * Numbers of feed.
    */
    count: {
      type: Number,
      default: 3,
      required: false
    },

    /*
     * Kinds of media to filter (Can be IMAGE, VIDEO, or CAROUSEL_ALBUM.).
     */
    mediatypes: {
      type: Array,
      default: () => ['IMAGE', 'VIDEO', 'CAROUSEL_ALBUM']
    },



    // class for container div
    containerClass: {
      type: String,
      default: '',
      required: false
    }
  },

  data: () => ({
    error: '',
    loading: false,
    feeds: []
  }),

  mounted () {
    // console.log('mounting vue-instagram...')
    this.getUserFeed()
  },

  methods: {
    getUserFeed () {
      // console.log('vue-instagram getting user feed...')
      this.loading = true

      const urlEndpoint = 'https://graph.instagram.com/me/media'
      const fields = (typeof this.fields == 'string') ? this.fields : this.fields.join(',')
      axios
        .get(urlEndpoint, {
          params: { access_token: this.token, fields: fields, count: this.count }
        })
        .then(response => {
          this.loading = false
          if (response.status === 400) this.error = response.statusText
          if (response.status === 200) {
            // console.log('vue-instagram data: ', response.data.data)
            for (const n in response.data.data) {
              if (this.mediatypes.includes(response.data.data[n].media_type)) {
                this.feeds.push(response.data.data[n])
                if (this.feeds.length >= this.count) {
                  return
                }
              }
            }
          }
        })
        .catch(error => { throw error })
    }
  }
}
</script>
