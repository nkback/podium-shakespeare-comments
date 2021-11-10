<template>
    <div style="display: flex; justify-content: center">
        <div>
            <!-- TODO: Pretty this up --> 
            <div>{{review.author}}</div>
            <div style="border: 1px solid grey; border-radius: 0 25px 25px 25px; width: 400px; padding: 25px">
                <div>Rating: {{review.rating}}</div>
                <div>Comment: {{review.body}}</div>
                 <!-- TODO: Make human readable --> 
                <div>Date: {{review.publish_date}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Review',
  props: {
    review: Object
  },
}
</script>