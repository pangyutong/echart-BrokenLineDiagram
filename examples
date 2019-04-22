<!--
  首页
-->

<script>
import Vue from 'vue'
import VueClassDecorator from 'vue-class-component'
import Echarts from 'echarts'
import $selfchart from '../chartEle'

const classPrefix = 'ad-home'

const DEFAULT_CHART = [{
  name: '展示量',
  key: 'pv',
  unit: '次',
  symbol: 'rect',
  color: '#2bbde6',
}, {
  name: '点击量',
  key: 'click',
  unit: '次',
  symbol: 'none',
  color: '#95e2af',
}, {
  name: '总花费',
  key: 'cost',
  unit: '元',
  symbol: 'triangle',
  color: '#ffd552',
}, {
  name: '点击率',
  key: 'ctr',
  unit: '%',
  symbol: 'diamond',
  color: '#fa6788',
}, {
  name: '千次平均展示价格',
  key: 'ecpm',
  unit: '元',
  symbol: 'circle',
  color: '#786de7',
}, {
  name: '平均点击价格',
  key: 'acpe',
  unit: '元',
  symbol: 'circle',
  color: '#e43c59',
}]

@VueClassDecorator({
  mixins: [],

  props: {},

  components: {},

  computed: {},

  watch: {},

  filters: {},

  methods: {},
})

export default class HomeTempalte extends Vue {
  indexData = {
    user: {
      state: {
        code: 0,
        label: ''
      },
      balance: 0
    },
    stat: {
      pv: 0,
      click: 0,
      cost: 0,
      ctr: 0,
      ecpm: 0,
      acpe: 0
    },
    chart: {
      time: [],
      pv: [],
      click: [],
      cost: [],
      ctr: [],
      ecpm: [],
      acpe: []
    }
  }

  // 过去14天趋势对比数据（默认）
  chartTypeA = 1 // 点击
  chartTypeB = 2 // 总花费

  formatNumberHandle(_val) {
    if (_val < 1000) {
      return _val
    } else if (_val >= 1000 && _val < 1000000) {
      while (/(\d+)(\d{3})/.test(_val.toString())) {
        _val = _val.toString().replace(/(\d+)(\d{3})/, '$1' + ',' + '$2')
        return _val
      }
    } else {
      while (/(\d+)(\d{3})(\d{3})/.test(_val.toString())) {
        _val = _val.toString().replace(/(\d+)(\d{3})(\d{3})/, '$1' + ',' + '$2' + ',' + '$3')
        return _val
      }
    }
  }

  getHomeDataHandle() {
    this.$S.INDEX_LIST().then(({data}) => {
      this.indexData = Object.assign({}, data)
      $selfchart.initChart(this.indexData.chart, DEFAULT_CHART, this.chartTypeA, this.chartTypeB, this.$refs.chart)
    }).catch(err => {
      this.$message.error(err.error_toast || err.message || '接口失败')
    })
  }

  chartTypeChangeHandle(_type, _val) {
    if (_type === 'A') {
      this.chartTypeA = _val
    } else {
      this.chartTypeB = _val
    }

    $selfchart.initChart(this.indexData.chart, DEFAULT_CHART, this.chartTypeA, this.chartTypeB, this.$refs.chart)
  }

  created () {
    this.getHomeDataHandle()
  }

  mounted () {}

  render (h) {
    const {
      indexData,
      formatNumberHandle,
      chartTypeA,
      chartTypeB,
      chartTypeChangeHandle
    } = this

    return <div class={classPrefix}>
      <el-card shadow="never" class={`${classPrefix}-account`}>
        <el-row>
          <el-col span={4}>账户状态：{indexData.user.state.label || '-'}</el-col>
          <el-col span={5}>账户余额：{indexData.user.balance || '0'}元</el-col>
        </el-row>
      </el-card>

      <el-card
        shadow="never"
        class={`${classPrefix}-data`}
        header="昨日概览"
      >
        <el-row gutter={20}>
          {
            DEFAULT_CHART.map((item) => {
              return (
                <el-col span={4} class="box">
                  <p>
                    <i>{item.name}</i>
                    <span>{formatNumberHandle(indexData.stat[item.key]) || '0'}</span>
                  </p>
                </el-col>
              )
            })
          }
        </el-row>
      </el-card>

      <el-card
        shadow="never">
        <div slot="header">
          <span>过去14天趋势</span>
          <div class={`${classPrefix}-select`}>
            <el-select
              name="selectA"
              value={chartTypeA}
              size='small'
              placeholder="请选择数据类别"
              on-change={chartTypeChangeHandle.bind(this, 'A')}
            >
              {
                DEFAULT_CHART.map((item, idx) => {
                  return (
                    <el-option
                      label={item.name}
                      value={idx}
                      disabled={idx === chartTypeB}
                    ></el-option>
                  )
                })
              }
            </el-select>
            <span>对比于</span>
            <el-select
              name="selectB"
              value={chartTypeB}
              size='small'
              placeholder="请选择数据类别"
              on-change={chartTypeChangeHandle.bind(this, 'B')}
            >
              {
                DEFAULT_CHART.map((item, idx) => {
                  return (
                    <el-option
                      label={item.name}
                      value={idx}
                      disabled={idx === chartTypeA}
                    ></el-option>
                  )
                })
              }
            </el-select>
          </div>
        </div>
        <div ref="chart" class={`${classPrefix}-chart`}>过去14天趋势图表</div>
      </el-card>
    </div>
  }
}
</script>

<style lang="less" scoped>
@class-prefix: ~'ad-home';

.@{class-prefix} {
  padding: 0 15px;

  &-account {
    margin-top: 15px;
    font-size: 16px;
    color: #333;
    line-height: 40px;
    vertical-align: middle;
  }

  &-data {
    margin-top: 15px;
    margin-bottom: 15px;

    p {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 80px;
      border-radius: 10px;
      background-color: #F2F6FC;
      text-align: center;
    }

    i {
      line-height: 34px;
      font-size: 14px;
      font-style: normal;
    }

    span {
      line-height: 34px;
      font-size: 24px;
    }
  }

  &-select {
    margin-top: -5px;
    float: right;

    span {
      padding: 0 10px;
      font-size: 12px;
      color: #666;
    }
  }

  &-chart {
    margin-top: 15px;
    height: 460px;
  }
}
</style>
