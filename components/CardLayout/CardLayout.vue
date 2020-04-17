<template>
  <div class="card">
    <div class="card-top">
      <button :class="liked | filterBtnLike"
              @click="changeLiked">
        <img src="~/assets/images/heart.svg" alt="">
      </button>
    </div>
    <div class="card-middle"></div>
    <div class="card-bottom">
      <InputField :type="'card'"
                  :placeholder="'0000  0000  0000  0000'"/>
      <InputField :type="'date'"
                  :placeholder="'00/00'"
                  :showSignature="true"
                  :signature="'VALID THRU'" :inline="true"/>
    </div>
  </div>
</template>

<script>
  import InputField from "../InputField/InputField";
  export default {
    name: "CardLayout",
    data () {
      return {
        liked: false
      }
    },
    filters: {
      /// filterBtnLike
      filterBtnLike (state) {
        return state ? 'card-like-btn active' : 'card-like-btn'
      },
      /*---------------------------------*/
    },
    methods: {
      /// changeLiked - понравилась ли карта?
      changeLiked () {
        this.liked = !this.liked
      },
      /*---------------------------------*/
    },
    components: {
      InputField
    }
  }
</script>
