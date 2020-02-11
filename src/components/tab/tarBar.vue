<template>
    <div class="tab">
        <cube-tab-bar
                :useTransition=true
                :showSlider=true
                v-model="selectedLabel"
                :data="tabs"
                ref="tabBar"
                class="border-bottom-1px">
        </cube-tab-bar>


        <div class="slide-wrapper">
            <cube-slide
                    :loop=false
                    :auto-play=false
                    :show-dots=false
                    :initial-index="index"
                    ref="slide"
                    :options="slideOptions"
                    @change="onChange">
                <cube-slide-item v-for="(tab,index) in tabs" :key="index">
                    <component ref="component" :is="tab.component" :data="tab.data"></component>
                </cube-slide-item>
            </cube-slide>
        </div>

    </div>
</template>

<script>
    export default {
        name: "tarBar",
        props:{
            tabs:{
              type:Array,
              default(){
                  return []
              }
            },
            initialIndex:{
                type:Number,
                default:0
            }
        },
        data() {
            return {
                index:this.initialIndex,
                slideOptions:{
                    listenScroll:true,
                    probeType:3,
                    directionLocked:0
                }
            }
        },
        methods: {
            clickHandler: function (lab) {
                console.log(lab)
            },
            onChange(cur){
                this.index = cur
                const component = this.$refs.component[cur]
                component.fetch && component.fetch()
                console.log(cur)
            },

        },
        computed: {
            selectedLabel: {
                get() {
                    return this.tabs[this.index].label
                },
                set(newVal) {
                    this.index = this.tabs.findIndex((value) => {
                        return value.label === newVal
                    })
                }
            }
        },

        mounted() {
            this.onChange(this.index)
        },
    }
</script>

<style scoped>

</style>
