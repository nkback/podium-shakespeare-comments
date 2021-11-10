<template>
    <div style="display: flex; justify-content: center">
        <div>
            <!-- TODO: Pretty this up --> 
            <div style="text-align: left; font-weight: bold">{{review.author}}</div>
            <div style="border: 1px solid grey; border-radius: 0 25px 25px 25px; width: 400px; padding: 25px">
              <div style="display: flex; justify-content: center">
                <div><span style="font-weight: bold">Date:</span> {{formattedDate(review.publish_date)}}</div>
                &nbsp;&nbsp;
                <div><span style="font-weight: bold">Rating:</span> {{review.rating}}</div>
              </div>
              <div style="margin-top: 8px"><span style="font-weight: bold">Comment:</span> {{review.body}}</div>
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
  methods: {
    formattedDate(date) {
      return new Date(date).toDateString(undefined, {
        year: "numeric",
        month: "long",
        day: "numeric"
      });
    }
  }
}
</script>