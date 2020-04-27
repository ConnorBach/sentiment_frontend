<template>
    <canvas width="50" height="50" ref="pie_chart"></canvas>    
</template>

<script>
import Chart from "chart.js"

export default {
    name: 'PieChart',
    props: {
        data: Object
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
                    data: this.displayData.data,
                    backgroundColor: this.displayData.backgroundColor
                }],
                labels: [
                    'Neutral',
                    'Bad',
                    'Good'
                ]
            }
            console.log(new_data)

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
        } },
    mounted: function() {
        this.drawChart()
    },
    updated: function() {
        console.log("updated")
        this.drawChart()
    },
    computed: {
        displayData: function() {
            return this.data
        }
    },
    watch: {
        $props: {
            handler() {
                this.drawChart()
            },
            deep: true,
            immediate: true
        }
    }
}
</script>

