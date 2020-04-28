<template>
    <div>
        <canvas width="50" height="50" ref="pie_chart"></canvas>    
    </div>
</template>

<script>
import Chart from "chart.js"

export default {
    name: 'PieChart',
    props: {
        isDelta: Boolean
    },
    data: function() {
        return {
            pieData: {}
        }
    },
    methods: {
        drawChart: function() {
            let ctx = this.$refs.pie_chart

            let new_data = {
                /*datasets: [{
                    data: [25, 25, 40],
                    backgroundColor: ["gray", "red", "green"]
                }],*/
                datasets: [{
                    data: this.pieData.data,
                    backgroundColor: this.pieData.backgroundColor
                }],
                labels: [
                    'Neutral',
                    'Bad',
                    'Good'
                ]
            }

            let options = {
                title: {
                    display: true,
                    text: 'Tweet Classification'
                }
            }
            new Chart(ctx, {
                type: 'doughnut',
                data: new_data,
                options: options
            });
        },
        getData: async function() {
            await fetch('http://127.0.0.1:5000/?query=' + this.queryString)
            .then((response) => {
                console.log(response)
                return response.json()
            })
            .then((rdata) => {
                console.log('data: ', rdata)

                let new_data = {}
                let data = [rdata["neutral"], rdata["negative"], rdata["positive"]]
                let backgroundColor = ["gray", "red", "green"]
                new_data.data = data
                new_data.backgroundColor = backgroundColor
                console.log(new_data)

                this.pieData = new_data
                return new_data
            })
        },
        refresh: async function() {
            await this.getData()
            this.drawChart()
        }
    },
    mounted: function() {
        this.refresh()
    },
    computed: {
        displayData: function() {
            return this.data
        },
        queryString: function() {
            return this.isDelta ? "\"Delta Airlines\"" : "\"United Airlines\""
        }
    },
    watch: {
        queryString: function() {
            this.refresh()
        }
    }
}
</script>

