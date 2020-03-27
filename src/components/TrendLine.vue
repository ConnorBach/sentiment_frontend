<template>
    <canvas width="50" height="50" ref="line_chart"></canvas>
</template>

<script>
import Chart from "chart.js"

export default {
    name: 'TrendLine',
    props: {},
    data: () => ({
        points: [{x:0, y: 10}, {x:1, y:15}, {x:2, y:35}, {x:3, y:20}]
    }),
    methods: {
        drawLine: function () {
            var ctx = this.$refs.line_chart
            //var points = [10, 15, 25, 20]

            /*
            new Chart(ctx, {
                type: 'line',
                data: points,
                options: {
                    title: {
                        display: true,
                        text: 'Sentiment'
                    },
                    scales: {
                        yAxes: [{
                            dispaly: true,
                            ticks: {
                                suggestedMin: 0,
                                suggestedMax: 50
                            }                            
                        }],
                    }
                }
            });*/

            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ["Mar 6", "Mar 7", "Mar 8", "Mar 9", "Mar 10", 
                    "Mar 11", "Mar 12", "Mar 13", "Mar 14"],
                    datasets: [{ 
                        data: [512,414,106,106,107,111,233,621,983,1012],
                        label: "Delta",
                        borderColor: "#3e95cd",
                        fill: false
                    }, { 
                        data: [303, 758, 493, 906, 169, 376, 547, 126, 933, 963],
                        label: "American",
                        borderColor: "#8e5ea2",
                        fill: false
                    }, { 
                        data: [310, 207, 407, 688, 732, 950, 618, 969, 747, 251],
                        label: "United",
                        borderColor: "#e8c3b9",
                        fill: false
                    }
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
    }
}

</script>

