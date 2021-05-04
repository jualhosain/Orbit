<template>
  <div id="orbit">
     <div class="orbit" :style="{'--font': display.percentageOfHeight/1.5+'px', '--hwCenter': display.percentageOfHeight*2+'px' }">
       <div v-for="value,b in innerDistance" :key="b">
          <div class="main--1" v-for="b,a in value" :key="b" :style="{'--width': display.percentageOfHeight*a+display.extra+'px', '--height': display.percentageOfHeight*a+display.extra+'px','--border': (a/50+0.001)+'px'}"  >
                <div class="main" :style="{'--animate' : a/10*6+6+'s'}" >
                 <Circle :data="b" :pH="display.percentageOfHeight" :dis="a" />

            </div>


        </div>
      </div>       

    </div>

  </div>
</template>

<script>
// import axios from 'axios';
import Circle from './components/circle'
import data from './assets/db.json'

export default {
  components: {
    Circle
  },
  data(){
    return {
      user: [],
      distance: [],
      display: [],
      innerDistance: [],
      userall: []
    }
  },
  methods: {
  },
    async created(){
      try{
    // const res = await axios.get('https://universaloffer.org/orbit/');
    //       this.user = [...res.data]
        // this.user = data;

          this.user = data.people;
          

          var w = window.innerWidth;
          var h = window.innerHeight;
          if(h < w){
               this.display = {height: h, width: w, workwith: h/100 *85, percentageOfHeight: (h/100 *85)/100, extra: (h/100 *5) }      
          }else{
               this.display = {height: h, width: w, workwith: w/100 *85, percentageOfHeight: (w/100 *85)/100, extra: (w/100 *5) }
          }
      

         this.user.forEach((e)=>{
            this.distance = [...this.distance, e.distance]
            this.distance = [...new Set(this.distance)]
            this.distance = this.distance.sort()
         });
        
        this.distance.forEach((a)=>{
         let userall = this.user.filter((user)=>{return a == user.distance;})
        this.innerDistance = [{ [a] : {...userall}},...this.innerDistance]
        })
        
        
        }
        catch(err){
            // console.log(err)
          }
    }
}
</script>

<style>
*{
  margin: 0 !important;
  padding:0 !important;;
  box-sizing: border-box;
}
#app {
  font-family:  arial, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#orbit{
  width: 100%;
  height: 100vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}


.orbit{
    width: var(--hwCenter);
    height: var(--hwCenter);
    border-radius: 50%!important;
    position: relative;
    background: green;
    color: white;
}
.orbit::before{
  content:"ME";
    font-size: var(--font);
    width: 100%;
    height: 100%;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;

}


@keyframes rotatt {
    0%{transform:rotate(0deg); }
    100%{transform:rotate(360deg);}
}



.main--1{
    width: var(--width);
    height: var(--height);
    position: absolute;
    top:calc(50% - var(--width)/2 );
    left:calc(50% - var(--width)/2);
    border-radius: 50%!important;
    border: var(--border) solid black;
}


.main{
    width: 100%;
    height: 100%;
    border-radius: 50%!important;
    position: relative;
     animation: rotatt var(--animate) infinite linear; 
    
} 

.one--o{
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: 0;
    border-radius: 50%!important;
    top:0;
    left:0;
    transform: rotate(calc(var(--two) * var(--one)));
}

.one--o::before{
    position: absolute;
    content: '';
    border-radius: 50%!important;
    top:calc(var(--width)/-1.8);
    left: calc(50% - var(--width)/2);
    width: var(--width);
    height: var(--height);
    background: white var(--img) no-repeat;
    object-fit: cover;
    object-position: center center;
    background-size: 100% 100%;
    border: var(--border) solid var(--color);
  
    z-index: 5;
    /* background: blue; */
    /* border: 5px solid var(--color); */
}



</style>
