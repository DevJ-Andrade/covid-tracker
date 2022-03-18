<template>
 <main v-if="!loading">
   <DataTitle :text="title" :dataDate="dataDate" />
      <div class="div-stats"></div>
      <div class="div-box">
      <h3>Cases </h3>
      
      <div class="div-third">
        <span>New:</span>
        {{ stats.NewConfirmed }}
      </div>
      <div class="div-third">
         <span>Total:</span>
        {{ stats.TotalConfirmed }}
      </div>
      </div>

      <!--Box 2 -->
      <div class="div-box2">
      <h3>Deaths </h3>
      
      <div class="div-third">
        <span>New:</span>
        {{ stats.NewDeaths }}
      </div>
      <div class="div-third">
         <span>Total:</span>
        {{ stats.TotalDeaths }}
      </div>
      </div>
  
   <DataBoxes :stats="stats" />

   <CountrySelect :countries="countries" />
</main>

<main v-else>
  <div class="div-main">
    Fetching Data
  </div>
  <img :src="loadingImage" alt="loading image" class="img-class">

</main>
</template>

<script>
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'

export default {
  name: 'HomeView',
  components: {
    DataTitle,
    DataBoxes
   },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '', 
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods: {
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json ()
      return data
    }
  },
  async created() {
    const data = await this.fetchCovidData()

    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.countries
    this.loading = false
},

}
</script>

<style scoped>
main{
  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.div-main{
  color:grey;
  font-size: 1.875rem;
  margin-top: 2.5rem;
  margin-bottom: 1.5rem;
}

.img-class {
  width: 6rem;
  margin: auto;
}
.div-stats {
display: flex;
flex-direction: column;
gap: 1rem;
background-color:red;

}

/* box */
.div-box {
background-color: rgb(219 234 254);
text-align:center;
border-radius: 0.25rem;
padding: 40px;
padding-left:200px;
padding-right:200px;
box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
margin-bottom: 16px;
}

h3 {
  	font-size: 1.875rem;
    line-height: 2.25rem;
    font-weight: bold;
    margin-bottom: 1rem;
    color: rgb(30, 58, 138);
    margin-bottom: 1rem;
}
.div-third {
	font-size: 1.5rem;
  line-height: 2rem;
  
}

span {
  font-weight:bold;
}

/* box 2 */
.div-box2 {
background-color: rgb(191 219 254);
text-align:center;
border-radius: 0.25rem;
padding: 40px;
padding-left:200px;
padding-right:200px;
box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
margin-bottom: 16px;
}

</style>

