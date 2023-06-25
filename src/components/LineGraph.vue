<template>
  <Line 
  class="graph"
    :options="chartOptions"
    :data="data"/>
</template>
  
<script>
import { Chart as ChartJS,CategoryScale, PointElement, LinearScale, Tooltip, Legend, LineElement } from 'chart.js';
import { Line } from 'vue-chartjs'

ChartJS.register(LineElement, CategoryScale, LinearScale, Tooltip, Legend, PointElement);
ChartJS.defaults.color = '#F1FFE0';

export default{
  name: 'LineChart',
  components: { Line },
    data() {
      return {
        data: {
          scaleLabel:{
          fontColor: '#F1FFE0'
          },
          labels: [
            '1.00','2.00','3.00','4.00','5.00','6.00','7.00','8.00','9.00','10.00','11.00','12.00',
            '13.00', '14.00', '15.00', '16.00', '17.00', '18.00', '19.00', '20.00', '21.00', '22.00', '23.00', '24.00',],
          datasets: [{
            type: 'line',
            label: 'traktor',
            data: [1, 1, 2, 0, 3],
            borderColor: 'green',
            backgroundColor: 'green'
          }, {
            type: 'line',
            label: 'gruz',
            data: [5, 2, 3, 0],
            fill: false,
            borderColor: 'blue',
            backgroundColor: 'blue'
          },
          {
            type: 'line',
            label: 'kran',
            data: [2, 2, 2, 2, 3, 1],
            borderColor: 'red',
            backgroundColor: 'red'
          },
          {
            type: 'line',
            label: 'ekskavator',
            data: [2, 2, 2, 1, 1, 1, 2, 3],
            borderColor: 'yellow',
            backgroundColor: 'yellow'
          },]
        },
        chartOptions: {
          responsive: true
          },

      }
    }
}

</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.graph{
  width: 100%;
  height: 60%;
  align-items: center;
  background-color: #27293D;
  margin-top: 1%;
  border-radius: 5px;
  color: #F1FFE0;
}
</style>