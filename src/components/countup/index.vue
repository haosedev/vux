<script>
import Countup from 'countup.js'

export default {
  name: 'countup',
  mounted () {
    this.$nextTick(() => {
      // this._countup = new Countup(this.$el, this.startVal, this.endVal, this.decimals, this.duration, this.options)
      // if (this.start) {
      //   this._countup.start()
      // }
      //**修改内容
      setTimeout(()=>{
        this._countup = new Countup(this.$el, this.startVal, this.endVal, this.decimals, this.duration, this.options)
        if (this.start) {
          this._countup.start()
        }
      },this.delay)
    })
  },
  props: {
    tag: {
      type: String,
      default: 'span'
    },
    start: {
      type: Boolean,
      default: true
    },
    startVal: {
      type: Number,
      default: 0
    },
    endVal: {
      type: Number,
      required: true
    },
    // number of decimal places in number
    decimals: {
      type: Number,
      default: 0
    },
    // duration in seconds
    duration: {
      type: Number,
      default: 2
    },
    options: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  render (h) {
    return h(this.tag, {}, [this.startVal])
  },
  watch: {
    start (val) {
      if (val) {
        this._countup.start()
      }
    },
    endVal (val) {
      //**修改内容
      //this._countup.update(val)
      this.$nextTick(() => {    //修改之后
        setTimeout(() => {
          this._countup.update(val)
        }, this.delay)
      })
    }
  }
}
</script>
