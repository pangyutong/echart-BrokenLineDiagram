import Echarts from 'echarts'

const $selfchart = {
  /**
 * @param {Array} _data 折线数据
 * @param {Number} _chartTypeA 左侧目标
 * @param {Number} _chartTypeB 右侧目标
 * @param {Object} _casebox refs
 */
  initChart(_data, _chartConfig, _chartTypeA, _chartTypeB, _casebox) {
    const myChart = Echarts.init(_casebox)

    window.onresize = myChart.resize;

    myChart.setOption({
      title: {
        text: ''
      },
      tooltip: {
        trigger: 'axis',
        axisPointer: {
          type: 'cross'
        }
      },
      legend: {
        bottom: 0,
        data: [_chartConfig[_chartTypeA]['name'], _chartConfig[_chartTypeB]['name']]
      },
      grid: {
        top: '6%',
        left: '5%',
        right: '5%',
        bottom: '10%',
        containLabel: true
      },
      xAxis: {
        type: 'category',
        boundaryGap: false,
        data: _data.time
      },
      yAxis: [{
        name: `${_chartConfig[_chartTypeA]['name']}（${_chartConfig[_chartTypeA]['unit']}）`,
        type: 'value',
        splitLine: {
          show: false
        }
      }, {
        name: `${_chartConfig[_chartTypeB]['name']}（${_chartConfig[_chartTypeB]['unit']}）`,
        type: 'value',
        splitLine: {
          show: false
        }
      }],
      series: [{
        name: _chartConfig[_chartTypeA]['name'],
        type: 'line',
        yAxisIndex: 0,
        areaStyle: {
          opacity: 0.2
        },
        symbol: _chartConfig[_chartTypeA]['symbol'],
        color: _chartConfig[_chartTypeA]['color'],
        data: _data[_chartConfig[_chartTypeA]['key']]
      }, {
        name: _chartConfig[_chartTypeB]['name'],
        type: 'line',
        yAxisIndex: 1,
        areaStyle: {
          opacity: 0.2
        },
        symbol: _chartConfig[_chartTypeB]['symbol'],
        color: _chartConfig[_chartTypeB]['color'],
        data: _data[_chartConfig[_chartTypeB]['key']]
      }]
    })
  }
}

export default $selfchart
