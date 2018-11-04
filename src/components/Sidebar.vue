<template>
    <div class="sidebar">
        <button class="btn_reset" @click="reset()">Reset filters</button>
        <hr>
        <div v-for="(category,j) in categories" :key="j" v-bind:id="category.label.normalize('NFD').replace(/[\u0300-\u036f]/g,'').replace(/\s/g,'_').toLowerCase()">
            <h3>{{ category.label }}</h3>
            <input v-if="!category.colors && !category.brands" v-bind:type="category.type" v-model="sdbar_price_value" @change="filters()">
            <span v-if="category.type == 'range'">{{ sdbar_price_value }}&euro;</span>
            <div v-if="category.colors" v-for="(color,i) in category.colors" :key="i" class="box_color_container">
                <input v-bind:type="category.type" class="hide" v-bind:id="'in_clr'+i" @change="filters()" v-model="checkedColors" v-bind:value="color">
                <label v-bind:for="'in_clr'+i" class="box_color" ><span v-bind:style="'background:'+color"></span></label>
            </div>
            <div v-if="category.brands" v-for="brand in category.brands" :key="brand">
                <input v-bind:type="category.type" v-bind:id="'in_brd_'+brand" @change="filters()" v-model="checkedBrands" v-bind:value="brand">
                <label v-bind:for="'in_brd_'+brand">{{ brand }}</label>
            </div>
            <hr>
        </div>
    </div>
</template>

<script>
    export default{
        props: ["categories"],
        data() {
            return{
                sdbar_price_value: 100,
                checkedBrands:[],
                checkedColors:[]
            }
        },
        methods: {
            filters() {
                this.$emit('filters', {
                    max_price: this.sdbar_price_value,
                    checkedBrands: this.checkedBrands,
                    checkedColors: this.checkedColors,
                    });
            },
            reset() {
                this.sdbar_price_value = 100;
                this.checkedBrands = [];
                this.checkedColors = [];
                this.filters();
            }
        }
    }
</script>

<style lang="scss">
@import "../assets/styles/reset.scss";
@import "../assets/styles/layout.scss";
.sidebar{
    width: 20%;
    position: absolute;
    top: 50px;
    bottom: 22px;
    min-width: 130px;
    padding: 5px;
    box-shadow: 0 0 15px rgba(0,0,0,.08), 0 0 4px rgba(0,0,0,.05);
    background: $white;
    z-index: 2;
    // text-align: left;
    h3{
        font-family: &title_font;
        font-weight: bold;
        text-align: center;
        width: 100%;
        padding-bottom: 10px;
        &::before{
            content: '\002702'; 
            display: inline-block; 
            position: relative; 
            top: 0px; 
            left: -10px; 
            color: $bleu; 
            font-size: 18px;
            font-weight: bold;
        }
    }
    .box_color_container{
        display: inline-block;
        margin: 5px;
        box-shadow: 0px 0px 6px 1px rgba(153,153,153,0.33);
        border: 1px solid #ddd;
    }
    .box_color{
        position: relative;
        height:20px;
        width:20px;
        display:block;
        > span {
            height:20px;
            width:20px;
            display: block;
        }
    }
    input[type=checkbox].hide{
        display:none;
        &:checked + .box_color span:before{
            content:'\2713';
            position:absolute;
            top:50%;
            left:50%;
            transform: translate(-50%,-50%);
            text-align: center;
            font-size:15px;
            color:rgb(235, 235, 235);
            border: 2px solid $bleu;
            height:20px;
            width:20px;
        }
    }
    input[type=range]{
        display: block;
        margin: auto;
        width: 80%;
        span{
            float: left;
        }
    }
    hr{
        border: none;
        border-top: 1px dashed #b7dfdf;
        margin-top: 10px;
    }
    div#brands > div{
    text-align: left;
    width: 80%;
    margin: auto;
    }
    .btn_reset {
        background: none;
        display: block;
        border: 2px solid;
        border-bottom-width: 4px;
        font: inherit;
        outline: none;
        margin: 15px auto;
        padding: 15px 20px;
        text-transform: inherit;
        transition: color 1s;
        $color: #eea163;
        color: $color;
        
        &:hover {
            animation: zigzag 1s linear infinite;
            background: linear-gradient(135deg, rgba($color,0.25) 0.25em, transparent 0.25em) -0.5em 0
                    , linear-gradient(225deg, rgba($color,0.25) 0.25em, transparent 0.25em) -0.5em 0
                    , linear-gradient(315deg, rgba($color,0.25) 0.25em, transparent 0.25em) 0 0
                    , linear-gradient(45deg, rgba($color,0.25) 0.25em, transparent 0.25em) 0 0;
            background-size: 0.75em 0.75em;
            color: adjust-hue($color,160);
        }
        }

        @keyframes zigzag {
        100% {
            background-position: 1em 0, 1em 0, -0.75em 0 , -0.75em 0;
        }
        }
}
</style>
