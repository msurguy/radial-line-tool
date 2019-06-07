<template>
  <path stroke="#000000" stroke-width="0.4mm" fill="none" :d="line"></path>
</template>

<script>
import { radialLine, curveCardinalClosed,
  curveBundle, curveLinear, curveLinearClosed, curveBasis,
  curveBasisOpen, curveBasisClosed, curveCardinal,
  curveCardinalOpen, curveCatmullRom, curveCatmullRomClosed,
  curveCatmullRomOpen, curveNatural, curveStepAfter, curveStepBefore, curveMonotoneX, curveStep } from 'd3'

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
        case 'curveBundle':
          return curveBundle
        case 'curveLinearClosed':
          return curveLinearClosed
        case 'curveBasisOpen':
          return curveBasisOpen
        case 'curveBasisClosed':
          return curveBasisClosed
        case 'curveCardinal':
          return curveCardinal
        case 'curveCardinalOpen':
          return curveCardinalOpen
        case 'curveCatmullRom':
          return curveCatmullRom
        case 'curveCatmullRomClosed':
          return curveCatmullRomClosed
        case 'curveCatmullRomOpen':
          return curveCatmullRomOpen
        case 'curveNatural':
          return curveNatural
      }
    }
  }
}
</script>
