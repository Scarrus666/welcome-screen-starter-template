<script>
export default 
  {
    name: "App",
    data() 
      {
        return {
          title: "Welcome to Opportunity",
          currentDate: new Date().toLocaleDateString("en-CH"), 
          sheet_id: import.meta.env.VITE_GOOGLE_SHEET_ID,
          api_token: import.meta.env.VITE_GOOGLE_API_KEY,
          entries_new: [],
          entries_test: "",
          transformedData: [],
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
              ],

              [
                "13:30",
                "07.09.2023",
                "Create a Google API Key",
                "Opportunity, Räffelstrasse"
              ],

              [
                "08:30",
                "12.09.2023",
                "Persönliche Präsentation (Mia)",
                "extern"
              ],

              [
                "08:30",
                "13.09.2023",
                "Testtitel",
                "extern"
              ],
            ],

         
        // transformedData:[],
        };
      },

    computed:
    {
      gsheet_url() 
        {
          //return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
          return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
        },

/*         console: () => console,
      window: () => window, */
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
          this.entries_new = data.valueRanges[0].values;

          console.log('entries: ' + this.entries_new);


          // manipulate the fetched data
          for (let i = 1; i < this.entries_new.length; i++) 
            {
              const [time, date, title, description] = this.entries_new[i];

              this.transformedData.push(
                {
                  time,
                  date,
                  title,
                  description,
                }
              );
            }

        }
    },


  };


</script>

<template>
  <div id="app">
    <h1 class="site-title">{{ title }}</h1>
    <h3 class="site-date">{{ currentDate }}</h3>

    <div class="cards" v-for="card in transformedData" v-if="transformedData">
      <div class="card">
        <ul>
          <li class="card-time">{{ card.time }} Uhr</li>
          <li class="card-title">{{ card.title }}</li>
          <li class="card-description">{{ card.description }}</li>
        </ul>
      </div>
    </div>
  </div>

  <footer>
    <div id="footer-logos">
      <img src="./assets/STZH_SEB_Logo.png" class="logoSTZ">
      <img src="./assets/Opportunity.png" class="logoOpprt">
      <img src="./assets/SAG_Logo_De.png" class="logoSAG">
    </div>
  </footer>
</template>

<style scoped>

#app 
{
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #323d4a;
  margin: 80px;
  min-height: 100vh;
}

main 
{
  flex-grow: 1; /* Allow the main content to grow and take remaining space */
}

.cards
{
  display: flex;
  justify-content: center;
}
.card
{
  width: 960px;
  height: 182px;
  background-color: #0F05A0;
  padding: 10px;
  margin-top: 15px;
  display: flex;
  align-items: center;
}

ul
{
  list-style-type: none;
}

.card-time
{
  color: #EB5E00;
  font-size: 28px;
  font-weight: 900;
}

.card-title
{
  color: #FFBFAB;
  font-size: 28px;
  font-weight: 900;
}

.card-description
{
  color: #FFBFAB;
  font-size: 28px;
  font-weight: 500;
}

.site-title
{
  color: #323D4A;
  font-size: 62px;
  font-weight: 900;
}
.site-date
{
  color: #9AA7B1;
  font-size: 62px;
  font-weight: 500;
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

#footer-logos
{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  margin: 10px;
  height: 100px;
}

.logoSTZ
{
  width: 230px;
  height: 44px;
}

.logoOpprt
{
  width: 296px;
  height: 55px; 
}

.logoSAG
{
  width: 273px;
  height: 52px;
}

.logoSTZ, .logoOpprt, .logoSAG 
{
  vertical-align: middle;
  max-height: 100%;
}

footer 
{
  /* position: fixed; */
  bottom: 0;
  margin: 0;
  width: 100%;
  height: 130px;
  background-color: #FFFFFF;
  flex-shrink: 0;
}

@media screen and (max-width: 768px) 
{
  /* Styles for screens up to 768px wide (typical tablet size) */
  #app 
  {
    margin: 20px; /* Adjust the margin for smaller screens */
  }
  
  .card 
  {
    width: 100%; /* Make cards take full width on smaller screens */
  }
  
  /* Adjust font sizes, padding, or any other styles as needed */

  footer 
  {
    height: auto; /* Allow the footer to adjust its height */
  }
  
  #footer-logos 
  {
    flex-direction: row; /* Stack logos vertically on smaller screens */
    align-items: center; /* Center align logos */
    margin: 10px;
  }
  
  .logoSTZ, .logoOpprt, .logoSAG 
  {
    width: auto; /* Allow logos to scale based on content */
    height: auto; /* Allow logos to scale based on content */
    max-width: 25%; /* Ensure logos don't exceed container width */
  }
}

@media screen and (max-width: 480px) 
{
  /* Styles for screens up to 480px wide (typical mobile size) */
  .site-title 
  {
    font-size: 36px; /* Reduce the font size for the site title */
  }
  
  .site-date 
  {
    font-size: 36px; /* Reduce the font size for the date */
  }

}

</style>
