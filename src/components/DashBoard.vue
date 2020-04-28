<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="blue"
      dark
    >
      <v-toolbar-title>Sentiment Dashboard</v-toolbar-title>
      <v-spacer />
        <v-autocomplete
        v-model="searchModel"
        :items="items"
        append-icon="mdi-magnify"
        >
        </v-autocomplete>
    </v-app-bar>

    <v-content>
        <v-row
          align="center"
          justify="center"
        >
          <v-col>
            <TrendLine :data="propsLineData"></TrendLine>
          </v-col>
          <v-col>
            <PieChart :isDelta="isDelta" :data="propsPieData"></PieChart>
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
      searchModel: null,
      deltaData: {
        pieData: {
          data: [50, 11, 37],
          backgroundColor: ["gray", "red", "green"]
        },
        lineData: {
          data: [512,414,106,106,107,111,233,621,983,1012],
          label: "Delta",
          borderColor: "#3e95cd",
          fill: false
        }
      },
      unitedData: {
        pieData: {
          data: [39, 23, 38],
          backgroundColor: ["gray", "red", "green"]
        },
        lineData: {
          data: [310, 207, 407, 688, 732, 950, 618, 969, 747, 251],
          label: "United",
          borderColor: "#e8c3b9",
          fill: false
        }
      },
      items: ['Delta', 'United'],
    }),
    computed: {
      isDelta: function() {
        if(this.searchModel == 'Delta') {
          return true
        } else {
          return false
        }
      },
      propsLineData: function() {
        return this.isDelta ? this.deltaData.lineData : this.unitedData.lineData
      },
      propsPieData: function() {
        return this.isDelta ? this.deltaData.pieData : this.unitedData.pieData
      }
    }
  }
</script>
