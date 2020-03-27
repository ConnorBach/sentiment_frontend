<template>
    <canvas width="50" height="50" ref="pie_chart"></canvas>    
</template>

<script>
import Chart from "chart.js"

export default {
    name: 'PieChart',
    methods: {
        drawChart: function() {
            let ctx = this.$refs.pie_chart

            let data = {
                datasets: [{
                    data: [25, 25, 40],
                    backgroundColor: ["gray", "red", "green"]
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
                data: data,
                options: options
            });
        } },
    mounted: function() {
        this.drawChart()
    }
}
</script>

