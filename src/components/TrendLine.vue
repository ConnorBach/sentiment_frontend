<template>
    <canvas width="50" height="50" ref="line_chart"></canvas>
</template>

<script>
import Chart from "chart.js"

export default {
    name: 'TrendLine',
    props: {
        data: Object
    },
    data: () => ({
    }),
    methods: {
        drawLine: function () {
            var ctx = this.$refs.line_chart
            let new_data = this.curData

            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ["Mar 6", "Mar 7", "Mar 8", "Mar 9", "Mar 10", 
                    "Mar 11", "Mar 12", "Mar 13", "Mar 14"],
                    datasets: [
                        new_data
                    ]
                },
                options: {
                    title: {
                    display: true,
                    text: 'Sentiment over Time'
                    }
                }
            });

        }
    },
    mounted: function() {
        this.drawLine()
    },
    computed: {
        curData: function() {
            return this.data
        }
    },
    watch: {
        curData: function() {
            this.drawLine();
        }
    }
}

</script>

