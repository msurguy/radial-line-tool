<template>
  <path stroke="#000000" stroke-width="0.4mm" fill="none" :d="line"></path>
</template>

<script>
import { radialLine, curveCardinalClosed, curveLinear, curveBasis, curveStepAfter, curveStepBefore, curveMonotoneX, curveStep } from 'd3'

export default {
  name: 'ClosedPolyline',
  props: {
    lineData: {
      type: Array,
      default: function () {
        return []
      }
    },
    roundness: {
      type: Number,
      default: 0.8
    },
    curve: {
      type: String,
      default: 'curveCardinalClosed'
    }
  },
  computed: {
    line () {
      console.log(this.curve)
      // let radialLineGenerator = radialLine().curve(curveCardinalClosed.tension(this.roundness))
      const path = radialLine()
        .curve(this.getCurve(this.curve))
      return path(this.lineData)
    }
  },
  methods: {
    getCurve (curveName) {
      switch (curveName) {
        case 'curveCardinalClosed':
          return curveCardinalClosed.tension(this.roundness)
        case 'curveLinear':
          return curveLinear
        case 'curveBasis':
          return curveBasis
        case 'curveStepAfter':
          return curveStepAfter
        case 'curveStepBefore':
          return curveStepBefore
        case 'curveMonotoneX':
          return curveMonotoneX
        case 'curveStep':
          return curveStep
      }
    }
  }
}
</script>
