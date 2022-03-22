<template>
    <div>
        <div v-for="data in tradeDataList.reverse()" :key="data">
            <div>
                {{ data.o.s }} - {{ data.o.p }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'App',
  data: () => {
    return {
      connection: null,
      tradeDataList: [],
    }
  },

  created() {
        this.getTradeStream();
    },

  methods: {
    getTradeStream() {

      console.log("Starting connection to WebSocket Server");
      this.connection = new WebSocket("wss://fstream.binance.com/ws/!forceOrder@arr");

      this.connection.addEventListener("message", (event) => {

        let tradeDataString = event.data;

        let parsedData = JSON.parse(tradeDataString);
        
        // push new item to array
        this.tradeDataList.push(parsedData);
        
        // keep only last 10
        this.tradeDataList = this.tradeDataList.slice(Math.max(this.tradeDataList.length - 20, 0))
      });

      this.connection.onopen = function(event) {
        console.log(event);
        console.log("Successfully connected to the echo websocket server...");
      };

    }
  }
}
</script>

<style>

</style>