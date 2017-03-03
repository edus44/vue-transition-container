<template>
    <div>   
        <template v-for="name in slotNames">
            <transition 
                @enter="enter" 
                @before-enter="beforeEnter" 
                @leave="leave" 
                :css="false"
                appear
            >
                <slot :name="name" v-if="visible"></slot>
            </transition>
        </template>

    </div>
</template>

<script>

import Velocity from 'velocity-animate'

export default {
    name: 'transition-container',
    props:['transition','visible'],
    data() {
        return {
            ps:['algo','otro']
        }
    },
    computed:{
        slotNames(){
            return Object.keys(this.$slots)
        }
    },
    methods: {
        beforeEnter(el){
          el.style.opacity = 0
        },
        enter: function (el, done) {
            let opts = getOptions(this,el)
            console.log(opts)
            Velocity(el, { 
                opacity: 1, 
                fontSize: '1.4em' 
            },{
                delay:500, 
                duration: 1000,
                complete: done 
            })
        },
        leave: function (el, done) {    
            Velocity(el, {
                rotateZ: '45deg',
                translateY: '30px',
                translateX: '30px',
                opacity: 0
            },{ 
                delay:500, 
                duration:1000,
                complete: done 
            })
        }
    }
}

function getOptions(vm,el){
    return{
        transition: el.getAttribute('transition') || vm.transition || 'fade',
        length: vm.slotNames.length,
        offset: el.getAttribute('offset')|0
    }
}
</script>