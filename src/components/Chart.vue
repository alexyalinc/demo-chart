<template>
  <div>
     <div class="box-info-container">
       <div class="box-info">
         <div class="box-count">+{{subs}}</div>
         <div class="box-title">просмотров</div>
       </div>
       <div class="box-info">
         <div class="box-count">+{{views}}</div>
         <div class="box-title">подписчиков</div>
       </div>
     </div>
    <div class="chart-container">
        <canvas id="chart" height="30vh" width="100vw"></canvas>
    </div>
  </div>
</template>

<script>
import Chart from "chart.js"
export default {
  name: 'Price',
  props: {
    price: {
      type: Number
    }
  },
  data () {
    return {
      chart: null,
      subs: 0,
      views: 0
    }
  },
  watch: {
    price: function (price) {
      this.updateGraphic(price)
    }
  },
  mounted() {
    this.createGraphic()
    this.updateGraphic(this.price)
  },
  methods: {
    createGraphic() {
      var ctx = document.getElementById('chart').getContext('2d');
      // disable legend and smoth line
      Chart.defaults.global.legend.display = false
      Chart.helpers.each(Chart.instances, function(chart) {
        chart.options.elements.line.tension =  .3;
        chart.update();
      });
      // gradient
      var gradientFill = ctx.createLinearGradient(0,0,0,150);
      gradientFill.addColorStop(0, "rgba(112, 69, 196, .5)");
      gradientFill.addColorStop(1, "rgba(112, 69, 196, .2)");
      this.chart = new Chart(ctx, {
          responsive: true,
          type: 'line',
          data: {
              labels: ['1 день', '2 день', '3 день', '4 день', '5 день', '6 день', '7 день'],
              datasets: [{
                  label: ' Просмотров',
                  data: [1, 3, 5, 5, 6, 8, 8],
                  borderColor: 'rgba(112, 69, 196, 1)',
                  pointBorderColor: 'rgba(112, 69, 196, 1)',
                  pointBackgroundColor: 'rgba(255, 255, 255, 1)',
                  pointHoverBackgroundColor: 'rgba(112, 69, 196, 1)',
                  pointHoverBorderColor: 'rgba(112, 69, 196, 1)',
                  backgroundColor: gradientFill,
                  borderWidth: 2
              }]
          },
          options: {
              scales: {
                  yAxes: [{
                      gridLines: {
                        display: false,
                      },
                      ticks: {
                        beginAtZero: true
                      }
                  }],
                  xAxes: [{
                      ticks: {
                        min: 0,
                        beginAtZero: false
                      }
                  }]
              }
          }
      });
    },
    updateGraphic(price) {
      let data = []
      let startNumber = Number(price)/10;
      let multiplier = 2;
      let quantity = 7;
      for (let i = 0; i < quantity; i++) {
        if (i > 3) {
          data.push(Math.floor(startNumber * multiplier * i))
        } else {
          data.push(Math.floor(startNumber * multiplier ** i))
        }
      }
      this.subs = data[6]
      this.views = data[6]/2
      this.chart.data.datasets[0].data = data
      this.chart.update()
    }
  }
}
</script>

<style scoped>
.chart-container {
  border: .1rem solid var(--grey-minor);
  box-sizing: border-box;
  border-radius: .6rem;
  padding-top: 1rem;
}
.box-info-container {
  display: flex;
  justify-content: flex-end;
}
.box-info {
  background: var(--violet-lilac-opacity);
  border-radius: .6rem;
  padding: 2rem 6rem;
  margin: 0 0 2rem 2rem;
  width: fit-content;
}
.box-count {
  font-style: normal;
  font-weight: bold;
  font-size: 3rem;
  line-height: 4rem;
  color: var(--black-main);
  text-align: center;
}
.box-title {
  font-family: Montserrat;
  font-style: normal;
  font-weight: 500;
  font-size: 1.8rem;
  line-height: 3.1rem;
  text-align: center;
}
@media only screen and (max-width: 1250px) {
  .box-info {
    width: 100%;
    margin: 0 0 2rem 0;
  }
  .box-info-container {
    margin: 2rem 0 0 0;
    flex-direction: column;
  }
  .chart-container {
    margin: 0 0 2rem 0;
  }
  #chart {
    max-height: fit-content;
  }
}
</style>
