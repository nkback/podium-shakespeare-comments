<template>
  <div class="hello">
    <h1>Yo</h1>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Home',
  data() {
    return {
      reviews: ''
    }
  },
  methods: {
    async getReviews() {
      let data = await axios.get("https://shakespeare.podium.com/api/reviews");
      console.log(data);
    }
  },
  props: {
    msg: String
  },
  mounted() {
    this.getReviews()
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
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
