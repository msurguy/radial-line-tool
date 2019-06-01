<template>
  <path stroke="#000000" stroke-width="0.4mm" fill="none" :d="line"></path>
</template>

<script>
import { range, scaleLinear, max, radialLine, curveBasisClosed } from 'd3'

export default {
  name: 'ClosedPolyline',
  props: {
    lineData: {
      type: Number,
      default: 0
    },
    roundness: {
      type: Number,
      default: 0.8
    }
  },
  computed: {
    line () {
      let minRange = 300
      let maxRange = 600
      let pathBreaks = 40
      let data = range(pathBreaks).map(function (d) {
        return d
      })

      let angle = scaleLinear()
        .domain([0, max(data)])
        .range([0, 2 * Math.PI])

      let radius = scaleLinear()
        .domain([0, max(data)])
        .range([minRange, maxRange])

      const path = radialLine()
        .angle((d) => { return angle(d) })
        .radius((d) => { return (this.lineData * 0.04 * radius(2 * Math.random())) })
        .curve(curveBasisClosed)
      // .curve(curveCardinalClosed.tension(0.8))

      return path(data)
    }
  }
}
</script>
