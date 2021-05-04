<template>
   <div v-for="a,b in data" :key="b" class="one--o" :style="{'--one':b,'--two':deg+'deg','--color':a.color,'--img':`url(${a.img_url})`,'--width': (dis/20)*pH+pH+'px','--height': (dis/20)*pH+pH+'px'}" ></div>
</template>

<script>
export default {
    name: 'circle',
    props: ['data','pH','dis'],
    data(){
        return{
            title : 'hello',
            count: 0,
            deg: 0,
            size: 0
        }
    },
    created(){
        let checkNum = 0;
       for (const key in this.data) {
            if(checkNum < key){
                checkNum = Number(key);
            }
       }
       this.count = 360/(checkNum+1);

        this.deg = 360/(checkNum+1);


    }
}
</script>

<style>

</style>