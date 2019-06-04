<template>
  <path stroke="#000000" stroke-width="0.4mm" fill="none" :d="line"></path>
</template>

<script>
import { range, scaleLinear, max, radialLine, curveBasisClosed } from 'd3'

export default {
  name: 'ClosedPolyline',
  props: {
    index: {
      type: Number,
      default: 0
    },
    roundness: {
      type: Number,
      default: 0.8
    },
    radiusFormula: {
      type: Number,
      default: 0
    }
  },
  computed: {
    line () {
      let pathBreaks = 10
      let data = range(pathBreaks).map(function (d) {
        return d
      })

      let angle = scaleLinear()
        .domain([0, max(data)])
        .range([0, 2 * Math.PI]) // replace 2 with curvature (0.1 - 4)

      const path = radialLine()
        .angle((d) => { return angle(d) })
        // lineData (counter) / 20 - 100 - spacing
        // replace 2 with a param (0, 4)
        .radius((d) => { return ((this.index * 4) * Math.random()) })
        .curve(curveBasisClosed)
      // .curve(curveCardinalClosed.tension(0.8))

      return path(data)
    }
  }
}
</script>
