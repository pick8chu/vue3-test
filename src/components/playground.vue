<template>
    <div>
        <h3>input data v-model test</h3>
        <div>
            <span>this data is ref</span><input v-model="inputData">
        </div>
        <div>
            <span>this data is not ref</span><input v-model="notRef">
        </div>
        <!-- <button>fix</button> -->
    </div>
    <div>
        <h3>data v-bind test</h3>
        <div>
            <span>ref: {{inputData}}</span>
        </div>
        <div>
            <span>not ref: {{notRef}}</span>
            <br/>
            since v-bind also have to be able to sense the changes of the variable, 
            <br/>
            although actual data has been changed, it won't be able to show with v-bind.
        </div>
        <!-- <button>fix</button> -->
    </div>
    <div>
        <h3>function test</h3>
        <button @click="changeValue">changeValue</button>
    </div>
    <div>
        <h3>
            computed test
        </h3>
        <span>ref: {{computedForInputData}}</span>
        <br/>
        <span>not ref: {{computedForNotRef}}</span>
    </div>
</template>

<script>
import {computed, ref, watch} from 'vue'

export default {
    name: 'PlayGround',
    setup(){
        // since ref is an "object", not a primitve type, const is the right choice.
        const inputData = ref("")
        const changeInputData = () => {
            inputData.value = "CHANGED"
        }
        watch(inputData, (cur, prev) => {
            console.log(`inputData: ${prev} -> ${cur}`)
        })
        
        /* ------------------ */

        const notRef = ""
        const changeNotRef = () => {
            // notRef = "CHANGED"
            // error  'notRef' is constant
        }

        const changeValue = () => {
            changeInputData()
            changeNotRef()
        }
        /* ------------------- */

        const computedForInputData = computed(()=>{
            return `"${inputData.value}" is the value of input data`
        })
        const computedForNotRef = computed(()=>{
            return `"${notRef}" is the value of input data`
        })

        return {
            inputData,
            notRef,
            changeValue,
            computedForInputData,
            computedForNotRef
        }
    }
}
</script>

<style>

</style>