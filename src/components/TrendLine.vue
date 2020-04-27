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
        points: [{x:0, y: 10}, {x:1, y:15}, {x:2, y:35}, {x:3, y:20}]
    }),
    methods: {
        drawLine: function () {
            var ctx = this.$refs.line_chart
            let new_data = this.data

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
    watch: {
        $props: {
            handler() {
                this.drawLine();
            },
            deep: true,
            immediate: true,
        },
    }
}

</script>

