<script>
import * as am5 from '@amcharts/amcharts5';
import * as am5xy from '@amcharts/amcharts5/xy';
import am5themes_Animated from '@amcharts/amcharts5/themes/Animated';


export default {
  
props: {
   clientes:Object,
   cecos:Object
  },

name: 'Graph',

mounted() {

    console.log('Mounted!');

    let root = am5.Root.new(this.$refs.chartdiv);

    root.setThemes([am5themes_Animated.new(root)]);

    let chart = root.container.children.push(
      am5xy.XYChart.new(root, {
         panX: false,
         panY: false,
         wheelX: "none",
         wheelY: "none",
         layout: root.verticalLayout
      })
    );

 // Create axes and their renderers
var yRenderer = am5xy.AxisRendererY.new(root, {
  visible: false,
  minGridDistance: 20,
  inversed: true
});

yRenderer.grid.template.set("visible", false);

var yAxis = chart.yAxes.push(
  am5xy.CategoryAxis.new(root, {
    renderer: yRenderer,
    categoryField: "category"
  })
);

var xRenderer = am5xy.AxisRendererX.new(root, {
  visible: false,
  minGridDistance: 30,
  inversed: true
});

xRenderer.grid.template.set("visible", false);

var xAxis = chart.xAxes.push(
  am5xy.CategoryAxis.new(root, {
    renderer: xRenderer,
    categoryField: "category"
  })
);


// Create series
// https://www.amcharts.com/docs/v5/charts/xy-chart/#Adding_series
var series = chart.series.push(
  am5xy.ColumnSeries.new(root, {
    calculateAggregates: true,
    stroke: am5.color(0xffffff),
    clustered: false,
    xAxis: xAxis,
    yAxis: yAxis,
    categoryXField: "x",
    categoryYField: "y",
    valueField: "value"
  })
);

series.columns.template.setAll({
  tooltipText: "{value}",
  strokeOpacity: 1,
  strokeWidth: 2,
  cornerRadiusTL: 5,
  cornerRadiusTR: 5,
  cornerRadiusBL: 5,
  cornerRadiusBR: 5,
  width: am5.percent(100),
  height: am5.percent(100),
  templateField: "columnSettings"
});

var circleTemplate = am5.Template.new({});

// Add heat rule
// https://www.amcharts.com/docs/v5/concepts/settings/heat-rules/
series.set("heatRules", [{
  target: circleTemplate,
  dataField: "value",
  key: "radius"
}]);



series.bullets.push(function () {
  return am5.Bullet.new(root, {
    sprite: am5.Label.new(root, {
      fill: am5.color(0xffffff),
      populateText: true,
      centerX: am5.p50,
      centerY: am5.p50,
      fontSize: 10,
      text: "{value}"
    })
  });
});

var colors = {
  critical: am5.color(0xca0101),
  bad: am5.color(0xe17a2d),
  medium: am5.color(0xe1d92d),
  good: am5.color(0x5dbe24),
  verygood: am5.color(0x0b7d03)
};

// Set data
// https://www.amcharts.com/docs/v5/charts/xy-chart/#Setting_data
var data = [
  {

    y: "Critical",
    x: "Very good",
    columnSettings: {
      fill: colors.medium
    },
    value: 20
  },
  {
    y: "Bad",
    x: "Very good",
    columnSettings: {
      fill: colors.good
    },
    value: 15
  },
  {
    y: "Medium",
    x: "Very good",
    columnSettings: {
      fill: colors.verygood
    },
    value: 25
  },
  {
    y: "Good",
    x: "Very good",
    columnSettings: {
      fill: colors.verygood
    },
    value: 15
  },
  {
    y: "Very good",
    x: "Very good",
    columnSettings: {
      fill: colors.verygood
    },
    value: 12
  },
  {
    y: "Critical",
    x: "Good",
    columnSettings: {
      fill: colors.bad
    },
    value: 30
  },
  {
    y: "Bad",
    x: "Good",
    columnSettings: {
      fill: colors.medium
    },
    value: 24
  },
  {
    y: "Medium",
    x: "Good",
    columnSettings: {
      fill: colors.good
    },
    value: 25
  },
  {
    y: "Good",
    x: "Good",
    columnSettings: {
      fill: colors.verygood
    },
    value: 15
  },
  {
    y: "Very good",
    x: "Good",
    columnSettings: {
      fill: colors.verygood
    },
    value: 25
  },
  {
    y: "Critical",
    x: "Medium",
    columnSettings: {
      fill: colors.bad
    },
    value: 33
  },
  {
    y: "Bad",
    x: "Medium",
    columnSettings: {
      fill: colors.bad
    },
    value: 14
  },
  {
    y: "Medium",
    x: "Medium",
    columnSettings: {
      fill: colors.medium
    },
    value: 20
  },
  {
    y: "Good",
    x: "Medium",
    columnSettings: {
      fill: colors.good
    },
    value: 19
  },
  {
    y: "Very good",
    x: "Medium",
    columnSettings: {
      fill: colors.good
    },
    value: 25
  },
  {
    y: "Critical",
    x: "Bad",
    columnSettings: {
      fill: colors.critical
    },
    value: 31
  },
  {
    y: "Bad",
    x: "Bad",
    columnSettings: {
      fill: colors.critical
    },
    value: 24
  },
  {
    y: "Medium",
    x: "Bad",
    columnSettings: {
      fill: colors.bad
    },
    value: 25
  },
  {
    y: "Good",
    x: "Bad",
    columnSettings: {
      fill: colors.medium
    },
    value: 15
  },
  {
    y: "Very good",
    x: "Bad",
    columnSettings: {
      fill: colors.good
    },
    value: 15
  },
  {
    y: "Critical",
    x: "Critical",
    columnSettings: {
      fill: colors.critical
    },
    value: 12
  },
  {
    y: "Bad",
    x: "Critical",
    columnSettings: {
      fill: colors.critical
    },
    value: 14
  },
  {
    y: "Medium",
    x: "Critical",
    columnSettings: {
      fill: colors.critical
    },
    value: 15
  },
  {
    y: "Good",
    x: "Critical",
    columnSettings: {
      fill: colors.bad
    },
    value: 25
  },
  {
    y: "Very good",
    x: "Critical",
    columnSettings: {
      fill: colors.medium
    },
    value: 19
  }
];

series.data.setAll(data);


yAxis.data.setAll([
  { category: "Critical" },
  { category: "Bad" },
  { category: "Medium" },
  { category: "Good" },
  { category: "Very good" }
]);

xAxis.data.setAll([
  { category: "Critical" },
  { category: "Bad" },
  { category: "Medium" },
  { category: "Good" },
  { category: "Very good" }
]);

// Make stuff animate on load
// https://www.amcharts.com/docs/v5/concepts/animations/#Initial_animation
chart.appear(1000, 100);

}}



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.graph {
  width: 100%;
  height: 500px;
}
</style>


<template>
  <div class="graph" ref="chartdiv">
  </div>

  <pre>{{clientes}}</pre>
</template>