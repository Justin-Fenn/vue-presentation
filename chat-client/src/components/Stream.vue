<template>
  <div class="stream">
    <ul>
      <li v-for="msg in messages">
        <message :message-in="msg" v-scroll-lock></message>
      </li>
    </ul>
  </div>
</template>

<script>

import Message from './Message';

export default {
  name: 'stream',
  components: {
    Message
  },
  computed: {
    messages() {
      return this.$store.getters.messages;
    }
  },
  directives: {
    scrollLock: {
      inserted: function(el){
        let containerElement = document.getElementsByClassName("stream")[0];
        containerElement.scrollTop = containerElement.scrollHeight;
      }
    }
  },
  created(){
    this.$store.dispatch('connectRoom', 'sample');
  }
};


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.stream {
  overflow-y: auto;
  
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 5px;
  background-color: #35495E;
}

@media only screen and (min-width: 900px) {
  .stream {
    width: 762px;
    margin: auto;
  }

}
</style>
