<template>
  <div class='container'>
    <div class="card py-4">
      <div>
        <button type="button" @click='setTimer(1000 * 5)' class="btn btn-outline-primary mx-3">5 Second</button>
        <button type="button" @click='setTimer(1000 * 30)' class="btn btn-outline-primary mx-3">30 seconds</button>
        <button type="button" @click='setTimer(1000 * 60)' class="btn btn-outline-primary mx-3">60 Second</button>
      </div>
      <div class="result m-5">
        <h2>
          {{timer}}
        </h2>
      </div>
      <div>
        <button class='btn btn-outline-info' @click='off'>Off</button>
      </div>
      
    </div>
    
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import "bootstrap/dist/css/bootstrap.css";
@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;

  timer : number = 0
  led : any
  setTimer (time : number) {
    this.timer = time / 1000
    let t = setInterval(()=>{
        this.timer--
        if(this.timer <= 0) {
            this.led.blink(1000 * 0.2);
            clearInterval(t)
        }
    },1000) 
           
  }

  off () {
    this.led.off()
  }

mounted () {
     boardReady({device: 'Jzv1'}, board => {
            board.systemReset();
            board.samplingInterval = 250;
            this.led = getLed(board, 10);
            console.log(this.led)
     })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
