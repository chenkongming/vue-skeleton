<template>
    <div  class='skeleton' :style="skeletonStyle">
        <div v-for="(item,index) in darks"
             class="item dark"
             :style="{ ...createStyle(item), backgroundColor: darkColor }"
             :key="'darks'+index">
        </div>
        <div v-for="(item,index) in lights"
             class="item light"
             :style="{ ...createStyle(item), backgroundColor: lightColor }"
             :key="'lights'+index">
        </div>
        <div v-for="(item,index) in squares"
             class="item square"
             :style="createStyle(item)"
             :key="'squares'+index">
        </div>
        <div v-for="(item,index) in circulars"
             class="item circular"
             :style="createStyle(item)"
             :key="'circulars'+index">
        </div>
        <div v-for="(item,index) in cylinders"
             class="item cylinder"
             :style="createCylinderStyle(item)"
             :key="'circulars'+index">
        </div>
    </div>
</template>

<script>
    // 约定.skeleton样式类为骨架屏查找绘制节点的根节点
    // 约定.skeleton-square 样式类，表示绘制当前节点的骨架节点样式为方形（如商品卡片）
    // 约定.skeleton-circular样式类，表示绘制当前节点的骨架节点为圆形（如logo）
    // 约定.skeleton-cylinder样式类，表示绘制当前节点的骨架节点为长条形（如搜索框）
    // 约定.skeleton-light与.skeleton-dark为块元素背景骨架样式
    export default {
        name: "Skeleton",
        data(){
            return{
                lights:[],
                darks: [],
                squares: [],
                circulars: [],
                cylinders: [],
            }
        },
        props:{
            selector: {
                 type:String,
                 required:false,
                 default:'skeleton'
            },
            backgroundColor: {
                type:String,
                required:false,
                default:'#fff'
            },
            lightColor: {
                type:String,
                required:false,
                default:'white'
            },
            darkColor: {
                type:String,
                required:false,
                default:'#2f3333'
            },
            top: {
                type:String,
                required:false,
                default:'0'
            },
        },
        mounted() {
            Promise.all([
                this.selectAll(`.${this.selector}-light`),
                this.selectAll(`.${this.selector}-dark`),
                this.selectAll(`.${this.selector}-square`),
                this.selectAll(`.${this.selector}-circular`),
                this.selectAll(`.${this.selector}-cylinder`),
            ]).then(([lights, darks, squares, circulars, cylinders]) =>{
                this.lights=lights
                this.darks=darks
                this.squares=squares
                this.circulars=circulars
                this.cylinders=cylinders
                }
            )
        },
        computed:{
            skeletonStyle(){
                return {
                    backgroundColor:this.backgroundColor,
                    top:this.top
                }
            }
        },
        methods: {
            selectAll(selector) {
                return new Promise(resolve =>{
                    let domList = document.querySelectorAll(selector)
                    let resultList = []
                    for(let a=0;a<domList.length;a++){
                        resultList.push(domList[a].getBoundingClientRect())
                    }
                    console.log('domList',domList)
                    resolve(resultList)
                  }
                )
            },
            createStyle({ width, height, top, left }){
               return {
                   width: `${width}px`,
                   height: `${height}px`,
                   top: `${top}px`,
                   left: `${left}px`,
               }
            },
            createCylinderStyle(rect){
                return {
                    ...this.createStyle(rect),
                    'border-radius': `${rect.height / 2}px`,
                }
            }
        }
    }
</script>

<style scoped lang="scss">
@import "./index";
</style>
