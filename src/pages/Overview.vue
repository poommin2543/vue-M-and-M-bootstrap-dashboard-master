<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col-xl-2 col-md-6">
          <stats-card>
            <div slot="header" class="icon-warning">
              <i class="nc-icon nc-support-17 colorm1"></i>
            </div>
            <div slot="content">
              <p class="card-category">SlotA</p>
              <h4 class="card-title">{{ m1 }}</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>{{ text }}
            </div>
          </stats-card>
        </div>

        <div class="col-xl-2 col-md-6">
          <stats-card>
            <div slot="header" class="icon-success">
              <i class="nc-icon nc-support-17 colorm2"></i>
            </div>
            <div slot="content">
              <p class="card-category">SlotB</p>
              <h4 class="card-title">{{ m2 }}</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>{{ text }}
            </div>
          </stats-card>
        </div>

        <div class="col-xl-2 col-md-6">
          <stats-card>
            <div slot="header" class="icon-danger">
              <i class="nc-icon nc-support-17 colorm3"></i>
            </div>
            <div slot="content">
              <p class="card-category">SlotC</p>
              <h4 class="card-title">{{ m3 }}</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>{{ text }}
            </div>
          </stats-card>
        </div>

        <div class="col-xl-2 col-md-6">
          <stats-card>
            <div slot="header" class="icon-info">
              <i class="nc-icon nc-support-17 colorm4"></i>
            </div>
            <div slot="content">
              <p class="card-category">SlotD</p>
              <h4 class="card-title">{{ m4 }}</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>{{ text }}
            </div>
          </stats-card>
        </div>
        <div class="col-xl-2 col-md-6">
          <stats-card>
            <div slot="header" class="icon-info">
              <i class="nc-icon nc-support-17 colorm5"></i>
            </div>
            <div slot="content">
              <p class="card-category">SlotE</p>
              <h4 class="card-title">{{ m5 }}</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>{{ text }}
            </div>
          </stats-card>
        </div>

        <div class="col-xl-2 col-md-6">
          <stats-card>
            <div slot="header" class="icon-info">
              <i class="nc-icon nc-support-17 colorm6"></i>
            </div>
            <div slot="content">
              <p class="card-category">SlotF</p>
              <h4 class="card-title">{{ m6 }}</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>{{ text }}
            </div>
          </stats-card>
        </div>

        <div class="col-xl-12 ">
          <stats-card>
            <div slot="header" class="icon-info">
              <i class="nc-icon nc-support-17 colorm1"></i>
              <i class="nc-icon nc-support-17 colorm2"></i>
              <i class="nc-icon nc-support-17 colorm3"></i>
              <i class="nc-icon nc-support-17 colorm4"></i>
              <i class="nc-icon nc-support-17 colorm5"></i>
              <i class="nc-icon nc-support-17 colorm6"></i>
              
            </div>
            <div slot="content">
              <p class="card-category">Total</p>
              <h4 class="card-title">{{ total }}</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>{{ text }}
            </div>
          </stats-card>
        </div>

      </div>
      <button type="button" class="btn btn-primary" @click="noom">click</button>
      <div class="row">
        <div v-if="grapestatus" class="col-md-8">
          <chart-card :chart-data="lineChart.data" :chart-options="lineChart.options"
            :responsive-options="lineChart.responsiveOptions">
            <template slot="header">
              <h4 class="card-title">Machine </h4>
              <p class="card-category">Performance</p>
            </template>
            <template slot="footer">
              <div class="legend">
                <i class="fa fa-circle colorm1"></i> SlotA
                <i class="fa fa-circle colorm2"></i> SlotB
                <i class="fa fa-circle colorm3"></i>SlotC
                <i class="fa fa-circle colorm4"></i> SlotD
                <i class="fa fa-circle colorm5"></i> SlotE
                <i class="fa fa-circle colorm6"></i> SlotF
              </div>
              <hr>
              <div class="stats">
                <i class="fa fa-history"></i> Updated 3 minutes ago
              </div>
            </template>
          </chart-card>
        </div>

        <div v-if="grapestatus" class="col-md-4">
          <chart-card :chart-data="pieChart.data" chart-type="Pie">
            <template slot="header">
              <h4 class="card-title">Email Statistics</h4>
              <p class="card-category">Last Campaign Performance</p>
            </template>
            <template slot="footer">
              <div class="legend">
                <i class="fa fa-circle colorm1"></i> SlotA
                <i class="fa fa-circle colorm2"></i> SlotB
                <i class="fa fa-circle colorm3"></i>SlotC
                <i class="fa fa-circle colorm4"></i> SlotD
                <i class="fa fa-circle colorm5"></i> SlotE
                <i class="fa fa-circle colorm6"></i> SlotF
              </div>
              <hr>
              <div class="stats">
                <i class="fa fa-clock-o"></i> Campaign sent 2 days ago
              </div>
            </template>
          </chart-card>
        </div>

      </div>


    </div>
  </div>
</template>
<script>
import ChartCard from 'src/components/Cards/ChartCard.vue'
import StatsCard from 'src/components/Cards/StatsCard.vue'
import LTable from 'src/components/Table.vue'
import mqtt from 'mqtt/dist/mqtt'
var one_day = 60 * 60 * 24
const today = new Date();
console.log(today / one_day)
export default {
  components: {
    LTable,
    ChartCard,
    StatsCard
  },
  data() {
    return {
      grapestatus :false,
      m1: 0,
      m2: 0,
      m3: 0,
      m4: 0,
      m5: 0,
      m6: 0,
      total:"N/a",
      editTooltip: 'Edit Task',
      deleteTooltip: 'Remove',
      pieChart: {
        data: {
          labels: ['SlotA', 'SlotB', 'SlotC', 'SlotD', 'SlotE', 'SlotF'],
          series: []
        }
      },
      text: "N/a",
      timeone: 0,
      timemqtt: 0,
      connection: {
        protocol: 'ws',
        host: '34.143.225.243',
        // ws: 8083; wss: 8084
        port: 9001,
        endpoint: '/mqtt',
        // for more options, please refer to https://github.com/mqttjs/MQTT.js#mqttclientstreambuilder-options
        clean: true,
        connectTimeout: 30 * 1000, // ms
        reconnectPeriod: 4000, // ms
        clientId:
          'emqx_vue_' +
          Math.random()
            .toString(16)
            .substring(2, 8),
        // auth
        username: 'test',
        password: 'Test123',
      },
      subscription: {
        topic: 'mandm/status',
        qos: 0,
      },
      publish: {
        topic: 'rover1/status',
        qos: 0,
        payload: 'Hi',
      },
      receiveNews: '',
      qosList: [0, 1, 2],
      client: {
        connected: false,
      },
      subscribeSuccess: false,
      connecting: false,
      retryTimes: 0,

      lineChart: {
        data: {

          labels: ['1', '2', '3', '4', '5', '6', '7', '8', 9],
          series: [
            [1,0,0,0,0,0,2,0,0],
            [0,2,0,0,0,0,0,3,0],
            [0,0,3,0,0,0,0,0,0],
            [0,0,0,4,0,0,0,0,4],
            [0,0,0,0,5,0,0,0,0],
            [0,0,0,0,0,6,0,0,0],
            
          ]
        },
        options: {
          low: 1,
          high: 6,
          showArea: false,
          height: '245px',
          axisX: {
            showGrid: false
          },
          lineSmooth: true,
          showLine: false,
          showPoint: true,
          fullWidth: true,
          chartPadding: {
            right: 50
          }
        },
        responsiveOptions: [
          ['screen and (max-width: 640px)', {
            axisX: {
              labelInterpolationFnc(value) {
                return value[0]
              }
            }
          }]
        ]
      },
      barChart: {
        data: {
          labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mai', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
          series: [
            [542, 443, 320, 780, 553, 453, 326, 434, 568, 610, 756, 895],
            [412, 243, 280, 580, 453, 353, 300, 364, 368, 410, 636, 695]
          ]
        },
        options: {
          seriesBarDistance: 10,
          axisX: {
            showGrid: false
          },
          height: '245px'
        },
        responsiveOptions: [
          ['screen and (max-width: 640px)', {
            seriesBarDistance: 5,
            axisX: {
              labelInterpolationFnc(value) {
                return value[0]
              }
            }
          }]
        ]
      },
      tableData: {
        data: [
          { title: 'Sign contract for "What are conference organizers afraid of?"', checked: false },
          { title: 'Lines From Great Russian Literature? Or E-mails From My Boss?', checked: true },
          {
            title: 'Flooded: One year later, assessing what was lost and what was found when a ravaging rain swept through metro Detroit',
            checked: true
          },
          { title: 'Create 4 Invisible User Experiences you Never Knew About', checked: false },
          { title: 'Read "Following makes Medium better"', checked: false },
          { title: 'Unfollow 5 enemies from twitter', checked: false }
        ]
      }
    }
  },
  mounted() {
    this.createConnection()
    // this.yourFunction()
    this.doSubscribe()
    // this.timenow()
    this.interval = setInterval(() => this.Checkonline(), 3000);

  },
  methods: {

    Checkonline() {

      if ((this.timenow() - this.timemqtt) > 0.1) {
        // console.log("Offline",(this.timenow()-this.timemqtt)*60)
        this.text = "offline"
      }

    },
    timenow() {

      var one_day = 60 * 60 * 24
      const today = new Date();
      // this.timeone=today/one_day
      return today / one_day
      // console.log(this.timeone)
    },
    initData() {
      this.client = {
        connected: false,
      }
      this.retryTimes = 0
      this.connecting = false
      this.subscribeSuccess = false
    },
    handleOnReConnect() {
      this.retryTimes += 1
      if (this.retryTimes > 5) {
        try {
          this.client.end()
          this.initData()
          this.$message.error('Connection maxReconnectTimes limit, stop retry')
        } catch (error) {
          this.$message.error(error.toString())
        }
      }
    },
    createConnection() {
      try {
        this.connecting = true
        const { protocol, host, port, endpoint, ...options } = this.connection
        const connectUrl = `${protocol}://${host}:${port}${endpoint}`
        this.client = mqtt.connect(connectUrl, options)
        if (this.client.on) {
          this.client.on('connect', () => {
            this.connecting = false
            console.log('Connection succeeded!')
          })
          this.client.on('reconnect', this.handleOnReConnect)
          this.client.on('error', error => {
            console.log('Connection failed', error)
          })
          this.client.on('message', (topic, message) => {
            this.receiveNews = this.receiveNews.concat(message)
            // console.log(`Received message ${message} from topic ${topic}`)
            console.log(`Received message ${message}`)
            this.text = "update"
            this.settext(message)

            // this.text = "OFF"

            this.timemqtt = this.timenow()
          })

        }
      } catch (error) {
        this.connecting = false
        console.log('mqtt.connect error', error)
      }
    },
    noom(){
      // this.lineChart.data.labels.push("10")
      console.log(this.lineChart.data.labels)
      this.grapestatus = true
      this.pieChart.data.series.push(m1*100/total)
    },
    // subscribe topic
    // https://github.com/mqttjs/MQTT.js#mqttclientsubscribetopictopic-arraytopic-object-options-callback
    settext(message) {
      const myArray = message.toString().split(":");
      if (myArray[0] == 'total'){
        this.total = myArray[1]
        this.lineChart.data.labels.push(myArray[1])
        
      }
      if (myArray[0] == 'm1'){
        this.m1 = myArray[1]
      }
      if (myArray[0] == 'm2'){
        this.m2 = myArray[1]
      }
      if (myArray[0] == 'm3'){
        this.m3 = myArray[1]
      }
      if (myArray[0] == 'm4'){
        this.m4 = myArray[1]
      }
      if (myArray[0] == 'm5'){
        this.m5 = myArray[1]
      }
      if (myArray[0] == 'm6'){
        this.m6 = myArray[1]
      }
      if (myArray[0] == 'reset'){
        this.m1 = 0
        this.m2 = 0
        this.m3 = 0
        this.m4 = 0
        this.m5 = 0
        this.m6 = 0
        this.total = "N/a"
      }

      // console.log(myArray[0])
      // console.log(myArray[1])
    },
    doSubscribe() {
      const { topic, qos } = this.subscription
      this.client.subscribe(topic, { qos }, (error, res) => {
        if (error) {
          console.log('Subscribe to topics error', error)
          return
        }
        this.subscribeSuccess = true
        console.log('Subscribe to topics res', res)
      })
    },
    // unsubscribe topic
    // https://github.com/mqttjs/MQTT.js#mqttclientunsubscribetopictopic-array-options-callback
    doUnSubscribe() {
      const { topic } = this.subscription
      this.client.unsubscribe(topic, error => {
        if (error) {
          console.log('Unsubscribe error', error)
        }
      })
    },
    // publish message
    // https://github.com/mqttjs/MQTT.js#mqttclientpublishtopic-message-options-callback
    doPublish() {
      const { topic, qos, payload } = this.publish
      this.client.publish(topic, payload, { qos }, error => {
        if (error) {
          console.log('Publish error', error)
        }
      })
    },
    // disconnect
    // https://github.com/mqttjs/MQTT.js#mqttclientendforce-options-callback
    destroyConnection() {
      if (this.client.connected) {
        try {
          this.client.end(false, () => {
            this.initData()
            console.log('Successfully disconnected!')
          })
        } catch (error) {
          console.log('Disconnect failed', error.toString())
        }
      }
    },
    handleProtocolChange(value) {
      this.connection.port = value === 'wss' ? '8084' : '8083'
    },
  },
}
</script>
<style>
.colorm1 {
  color: rgb(255, 0, 0);
}

.colorm2 {
  color: rgb(34, 0, 255);
}

.colorm3 {
  color: rgb(137, 134, 132);
}

.colorm4 {
  color: rgb(228, 214, 24);
}

.colorm5 {
  color: rgb(0, 255, 55);
}

.colorm6 {
  color: rgb(0, 0, 0);
}</style>
