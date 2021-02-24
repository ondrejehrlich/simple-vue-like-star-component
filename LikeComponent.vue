<template>
  <div class="like-component-container">
    <a @click="likeToggle()" :title="title">
      {{ number }}
      <i :class="fontClass"></i>
    </a>
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    likeable: {
      type: String,
    },
    likeableId: {
      type: Number,
    },
    likesNumber: {
      type: Number,
      default: 0,
    },
    hasLiked: {
      type: Boolean,
      default: false,
    },
    guest: {
      type: Boolean,
      default: false,
    },
    apiUrl: {
      type: String,
      default: "/api/like",
    },
    likedClass: {
      type: String,
      default: "mdi mdi-star",
    },
    dontLikedClass: {
      type: String,
      default: "mdi mdi-star-outline",
    },
  },

  data() {
    return {
      liked: false,
      number: parseInt(this.likesNumber),
      id: parseInt(this.likeableId),
      title: "",
    }
  },

  computed: {
    fontClass() {
      if (this.liked) {
        return "liked " + "mdi mdi-star"
      } else return "dont-liked " + "mdi mdi-star-outline"
    },
  },

  methods: {
    likeToggle() {
      if (this.guest) {
        return
      }
      if (this.liked) {
        this.removeLike()
      } else if (!this.liked) {
        this.addLike()
      }
    },

    addLike() {
      axios
        .post(this.apiUrl, {
          likeable: this.likeable,
          id: this.id,
        })
        .then((res) => {
          this.liked = true
          this.number = res.data.likes
        })
    },

    removeLike() {
      axios
        .delete(this.apiUrl, {
          data: {
            likeable: this.likeable,
            id: this.id,
          },
        })
        .then((res) => {
          this.liked = false
          this.number = res.data.likes
        })
    },
  },

  beforeMount() {
    this.title = this.guest ? "You have to be logged in to add star." : ""

    if (this.hasLiked === "true" || this.hasLiked === true) {
      this.liked = true
    } else {
      this.liked = false
    }
  },
}
</script>

<style lang="scss" scoped>
.like-component-container {
  margin-left: 0.6em;

  .liked,
  .dont-liked {
    font-size: 200%;
  }

  .liked {
    color: rgb(255, 159, 37);
  }

  .dont-liked {
    color: #666;
  }
}
</style>
