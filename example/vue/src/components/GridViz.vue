<template>
<div>
    <h1>Traces</h1>
    <div id="traces">
        <div v-for="(t, tId) in traces" :key="tId">
            <Trace :trace="t" :info="info" :size="traceSize" :tId="tId">
        </div>
    </div>
</div>
</template>

<script>
import Trace from './Trace.vue'

export default {
  name: 'GridViz',
  components: {Trace},
  data() {
    return {
      windowSize: {height: window.innerHeight, width: window.innerWidth},
    }
  },
  props: ['traces', 'info'],
  computed: {
      traceSize() {
        let numTraces = Object.keys(this.traces).length
        let perRow = numTraces < 5 ? numTraces : 5
        let numRows = Math.ceil(numTraces / perRow)
        let suggestedHeight = this.windowSize.height / numRows;
        let suggestedWidth = (this.windowSize.width - 10) / perRow;
        return {h: suggestedHeight, w: suggestedWidth}
      }
  },
  mounted () {
    this.$nextTick(() => {
        window.addEventListener('resize', () => {
            this.windowSize = {height: window.innerHeight, width: window.innerWidth};
        })
    })
  }
}
</script>

<style>
html, body {
    margin-left: 0;
    margin-right: 0;
}
</style>

<style scoped>
h1 {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    text-align: center;
}
#traces {
    display: flex;
    flex-flow: row wrap;
}

</style>