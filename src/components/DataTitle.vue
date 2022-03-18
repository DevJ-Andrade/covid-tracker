<template>
  <div class="div-template">
      <h2> {{text}}</h2>
      <div class="div-date">{{ timestamp }}</div>
  </div>
</template>

<script>
import moment from 'moment'

export default {

name: 'DateTitle',
props: ['text', 'dataDate'],
computed: {
    timestamp: function() {
        return moment(this.dataDate).format('MMMM DD YYYY, h:mm:ss a')
    },
},
}

</script>

<style>
.div-template {
    text-align: center;
}
h2{
    font-size: 1.875rem;
    line-height: 2.25rem;
    font-weight: bold;
}
.div-date {
    font-size: 1.5rem;
    line-height: 2rem;
}
</style>