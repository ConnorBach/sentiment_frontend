<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="blue"
      dark
    >
      <v-spacer />
      <v-toolbar-title>Sentiment Dashboard</v-toolbar-title>
    </v-app-bar>

    <v-content>
        <v-row
          align="center"
          justify="center"
        >
          <v-col>
            <TrendLine></TrendLine>
          </v-col>
          <v-col>
            <PieChart></PieChart>
          </v-col>
        </v-row>
    </v-content>
  </v-app>
</template>

<script>
  import TrendLine from "./TrendLine"
  import PieChart from "./PieChart"

  export default {
    name: 'DashBoard',
    components: {
      TrendLine,
      PieChart
    },
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
    }),
  }
</script>
