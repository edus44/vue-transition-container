<template>
    <div>
        <transition-container transition="fade" :visible="visible">
            <div slot="1" offset="1">app</div>
            <div slot="2" offset="2" transition="grow">app2</div>
            <div slot="3" offset="2" transition="grow">app2</div>
            <div slot="" offset="3">app3</div>
            <p v-for="p,index in ps" :slot="'a'+index" :offset="index+4" transition="otheranim">
                {{p}}
            </p>
        </transition-container>
        <button @click="visible=!visible">toggle</button>
    </div>
</template>


<script>
import TransitionContainer from './TransitionContainer'

export default {
    name: 'App',
    data:()=>({
        visible:true,
        ps:['algo1','algo2']
    }),
    components: {TransitionContainer}
} 
</script>
