<template>
  <div>
    <p>{{status}}</p>
    <!-- eslint-disable -->
    <h1>
      {{ minit < 10 ? "0" + minit : minit }}:{{
        second < 10 ? "0" + second : second
      }}
    </h1>
    <!-- eslint-enable -->
    <p>Session Length</p>
    <span
      ><button @click="defaultsession != 1 ? defaultsession-- : defaultsession">
        -</button
      >{{ defaultsession }}<button @click="defaultsession++">+</button></span
    >
    <p>Break Length</p>
    <span
      ><button @click="defaultbreak != 1 ? defaultbreak-- : defaultbreak">
        -</button
      >{{ defaultbreak }}<button @click="defaultbreak++">+</button></span
    >
    <br />
    <span id="twinbuttons"><button  @click="countdown() ; play()" v-if="active">Start</button>
    <button v-else @click="pause">Pause</button>
    <button @click="reset">Reset</button>
    </span>
  </div>
</template>

<script>
var countdowntimer = null
export default {
  data() {
    return {
      minit: 0,
      second: 0,
      defaultsession: 10,
      defaultbreak: 5,
      active:true,
      kickstart: true,
      clonesession: null,
      status:""
    };
  },
  methods: {
    countdown() {
      if (this.kickstart == true) {
        this.status="Woke"
        this.clonesession = this.defaultsession;
        this.minit = this.clonesession;
        setTimeout(function () {
          that.minit--;
          that.clonesession--;
          that.second = 60;
        }, 1000);
        this.kickstart = false;
      }
      let that = this;
      countdowntimer = setInterval(() => {
        if (this.second == 0 && this.minit != 0) {
          clearInterval(countdowntimer);
          this.clonesession--;
          this.minit = this.clonesession;
          this.second = 59;
          this.countdown();
        } else if (this.second == 0 && this.minit == 0 && this.status == "Woke") {
          this.status="i sleep"
          // this.kickstart = false
          this.breakcountdown();
        }
        else if (this.second == 0 && this.minit == 0 && this.status == "i sleep") {
          clearInterval(countdowntimer)
          this.addcycle();
          this.countdown();
          this.kickstart = true
        }
         else {
          --this.second;
        }
      }, 1000);
    },
    breakcountdown(){
        this.clonesession = this.defaultbreak;
        this.minit = this.clonesession;
        // setTimeout(function () {
        //   that.clonesession--;
        //   that.second = 59;
        // }, 1000);
        
      
      // let that = this;
    },
    pause(){
      this.active = !this.active;
      clearInterval(countdowntimer)
    },
    play() {
      this.active = !this.active;
    },
    addcycle() {
      this.$emit('addcycle')
    },
    reset() {
      clearInterval(countdowntimer)
      this.minit = 0;
      this.second = 0;
      this.kickstart= true
      this.clonesession= null
      this.status="";
      this.active=true;
      this.$emit('resetcycles')
    }
  }
};
// };
</script>

<style scoped>
div {
  border-style: solid;
  border-radius: 25px;
  padding: 40px;
  display:flex;
  align-items: center;
  flex-direction: column;
  text-align: center;
  height: 300px;
}
</style>