<template>
  <div>
    <div class="section-heading">
      <p class="heading">
        {{ this.title }}
        <span> {{ this.description }} </span>
      </p>
      <p class="period"></p>
    </div>
    <GChart
      type="LineChart"
      :data="chartData"
      :options="chartOptions"
    />    
  </div>
</template>

<script>
// import { GChart } from "vue-google-charts";
import moment from "moment";

export default {
  name: "LineGchart",
  components: {
    // GChart
  },
  props: {
      values: Array,
      metrics: Array,
      title:String,
      description:String,
      xname:String,
      yname:String
   },
  data() {
    return {
      // Array will be automatically processed with visualization.arrayToDataTable function
      chartData:[
          [this.xname, this.yname],
          ...this.values.map((value,i,arr) => [moment(value.category).format("DD MMM YYYY"),arr[parseInt(i)][this.metrics[0]]?arr[parseInt(i)][this.metrics[0]]:0])
      ],
      chartOptions: {
        chart: {
          title: "Company Performance",
          subtitle: "Sales, Expenses, and Profit: 2014-2017",
          isStacked: true
            }
        }
    };
  },
  mounted (){
  }
};
</script>
