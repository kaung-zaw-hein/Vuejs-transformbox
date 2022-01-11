<template>
  <main>
       <section class="settings">
            <div class="settings-container">
            <label>perspective: {{ perspective }}px;</label>
            <input type="range" min="0" max="999" v-model="perspective" />

            <label>rotateX: {{ rotateX }}deg; </label>
            <input type="range" min="-180" max="180" v-model="rotateX" />

            <label>rotateY: {{ rotateY }}deg; </label>
            <input type="range" min="-180" max="180" v-model="rotateY" />

            <label>rotateZ: {{ rotateZ }}deg; </label>
            <input type="range" min="-180" max="180" v-model="rotateZ" />

                <div>
                    <button type="button" @click.prevent="reset">Reset</button>
                <button type="button" @click.prevent="copy">Copy</button>
                </div>
            </div>
        </section>
        <section class="output">
            <div class="box-container">
            <div  class="box" :style="box"></div>
            </div>
        </section>
  </main>
</template>

<script>
import {ref,computed} from "vue"
export default {
    setup(){
        let perspective = ref(100);
        let rotateX = ref(0);
        let rotateY = ref(0);
        let rotateZ = ref(0);
        let box = computed(() => {
             return {
                transform: `
                perspective(${perspective.value}px)
                rotateX(${rotateX.value}deg)
                rotateY(${rotateY.value}deg)
                rotateZ(${rotateZ.value}deg)
                `
            };
        })
        let reset = () => {
            perspective.value = 100;
            rotateX.value = 0;
            rotateY.value = 0;
            rotateZ.value = 0;
                
        }
        let  copy = () => {
            const el = document.createElement('textarea')

            el.setAttribute('readonly', '')
            el.style.position = 'absolute'
            el.style.left = '-9999px'
            el.value = `transform: 
                perspective(${perspective.value}px)
                rotateX(${rotateX.value}deg)
                rotateY(${rotateY.value}deg)
                rotateZ(${rotateZ.value}deg)`

            document.body.appendChild(el)
            el.select()
            document.execCommand('copy')
            document.body.removeChild(el)
        }
        return {perspective,rotateX,rotateY,rotateZ,box,reset,copy}
    }
    
}
</script>

<style>
    section{
        width: 50%;
    }
    .settings-container{
        display: flex;
        flex-direction:column;
        text-align: left;
    }  
    label{
        font-size:1.5em;
        font-weight:100px;
        color:rgb(255, 255, 255);
        margin: 15px 0;
    }
    input[type="range"] {
    width:250px;
    -webkit-appearance: none;
    }

    input[type="range"]:focus {
    outline: none;
    }

    input[type="range"]::-webkit-slider-runnable-track {
    background: rgb(0, 0, 0);
    height: 3px;
    }

    input[type="range"]::-moz-range-track {
    background: #999;
    height: 3px;
    }

    input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    height: 15px;
    width: 15px;
    background: #fff;
    margin-top: -6px;
    border-radius: 50%;
    border: 2px solid #111;
    cursor: pointer;
    }

    input[type="range"]::-moz-range-thumb {
    height: 15px;
    width: 15px;
    background: #111;
    margin-top: -6px;
    border-radius: 50%;
    border: 2px solid #111;
    cursor: pointer;
    }
    button{
        margin:20px 0;
        width:135px;
        color:#fff;
        background: rgb(15, 0, 0);
        border-radius: 4px;
        border: 2px solid #fff;
    }
    .box-container {
  padding: 50px;
  border: 1px solid #000000;
  height:50%;
    }
    .box {
    width: 150px;
    height: 150px;
    background: #000000;
    margin: auto;
    }
</style>