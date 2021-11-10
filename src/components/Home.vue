<template>
  <div>
    <div style="display: flex; width: auto; justify-content: center; margin-bottom: 35px">
      <div style="font-size: 28px; display: flex; flex-direction: column; align-items: center; justify-content: center"><div>Avg Rating:</div><div>{{this.average}}</div></div>
      &nbsp;&nbsp;&nbsp;&nbsp;
      <img alt="Vue logo" src="../assets/shakespeare.jpg" style="height: 200px;">
    </div>
    <div> 
      <input type="text" style="width: 452px; height: 30px; border-radius: 8px; border: solid 1px gray; margin-bottom: 8px" placeholder="Search name or content of a review" v-model="search" @input="debounceInput" />

    </div>
    <div v-for="review in filteredReviews" :key="review.id">
      <Review :review="review" style="margin-bottom: 15px" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Review from './Review.vue'
import _ from 'lodash';

export default {
  name: 'Home',
  components: {Review},
  data() {
    return {
      reviews: [],
      filteredReviews: [],
      average: 0.0,
      search: ''
    }
  },
  methods: {
    async getReviews() {
      let res = await axios.get("https://shakespeare.podium.com/api/reviews");
      if(res.status === 200) {
        this.reviews = res.data
        this.filteredReviews = res.data
      }
      this.calcAvg()
    },
    calcAvg() {
      let total = 0;

      this.reviews.forEach(item => {
        total += item.rating
      });

      this.average = (total / this.reviews.length).toFixed(2)
    },
    debounceInput: _.debounce(function () {
      if(this.search === '') this.filteredReviews = this.reviews;
      else {
        this.filteredReviews = this.reviews.filter((item) => {
          return item.body.toLowerCase().includes(this.search.toLowerCase()) || item.author.toLowerCase().includes(this.search.toLowerCase())
        })
      }
    }, 500)
  },
  mounted() {
    axios.defaults.headers.common['x-api-key'] = 'H3TM28wjL8R4#HTnqk?c'
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
