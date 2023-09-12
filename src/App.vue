<script>
export default 
  {
    name: "App",
    data() 
      {
        return {
          title: "Welcome to Opportunity",
          sheet_id: import.meta.env.VITE_GOOGLE_SHEET_ID,
          api_token: import.meta.env.VITE_GOOGLE_API_KEY,
          entries: 
            [
              [
                  "15:15",
                  "06.09.2023",
                  "Pause",
                  "Opportunity, Räffelstrasse 12"
              ],

              [
                  "15:30",
                  "06.09.2023",
                  "Start Vue Welcome Screen Project",
                  "Opportunity, Räffelstrasse 12"
              ],

              [
                  "15:35",
                  "06.09.2023",
                  "Live Demo Welcome Screen",
                  "Opportunity, Räffelstrasse 12"
              ],

              [
                  "16:00",
                  "06.09.2023",
                  "Create a Google API Key",
                  "Opportunity, Räffelstrasse 12"
              ]
            ],
        // transformedData:[],
        };
      },

      mounted() 
        {
          this.getData(); // get first initial data and then wait for the next update
        },

      methods: 
      {
        async getData()  
          {
            const response = await fetch(this.gsheet_url);
            const data = await response.json();
            this.entries = data.valueRanges[0].values;
          }
    },
  };


</script>

<template>
  <div id="app">
    <h1 class="site-title">{{ title }}</h1>
    
  </div>
</template>

<style scoped>

#app 
{
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #323d4a;
  background-color: lightcyan;
  margin: 60px;
  font-size: 62px;
}
.card
{
  background-color: darkblue;
  padding: 10px;
  margin-top: 15px;
}
.site-date
{
  color: grey;
}
.timeStamp
{
  color: tomato;
  font-weight: bold;
  font-size: large;
}
.cardTitle
{
  color: lightsalmon;
  font-size: large;
  font-weight: bold;
}
.cardBeschreibung
{
  color: lightcoral;
}

#footerLogos
{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin: 10px;
  color: darkblue;
}
.logosSponsors
{
  width: 200px;
  height: 50px;
}

footer 
{
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: white;
}

</style>
