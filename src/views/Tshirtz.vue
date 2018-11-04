<template>
    <div class="tshirtz">
        <sidebar :categories="categories" v-on:filters="filtered($event)"></sidebar>
        <main class="content">
            <article class="tshirt_article" v-for="(tshirt,i) in tshirt_products_toshow" :key="i">
                <h3>{{ tshirt.name }}</h3>
                <div class="picture">
                    <img v-bind:src="tshirt.img_url" alt="consume photo">
                </div>
                <p>{{ tshirt.price }}&euro;</p>
            </article>
        </main>
    </div>
</template>

<script>
import sidebar from "@/components/Sidebar.vue"
    export default{
        components: {
            sidebar
        },
        data() {
            return{
                tshirt_products:[
                    {name:'Harold Hunter',
                    price:20,
                    brand:'obey',
                    color: 'white',
                    img_url:'https://lauriannel.com/teeshirtz/img/HaroldHunter_white.jpg'
                    },
                    {name:'Harold Hunter',
                    price:22,
                    brand:'obey',
                    color: 'black',
                    img_url:'https://lauriannel.com/teeshirtz/img/HaroldHunter_black.jpg'
                    },
                    {name:'consume',
                    price:24.99,
                    brand:'obey',
                    color: 'gray',
                    img_url:'https://lauriannel.com/teeshirtz/img/Consume_gray.jpg'
                    }
                    ],
                categories: [
                    {label:'Price max',
                    type: 'range'
                    },
                    {label:'Brands',
                    type: 'checkbox',
                    brands:['obey', 'zoo york', 'The Kooples', 'element', 'cbgb', 'dickies']
                    },
                    {label:'Colors',
                    type: 'checkbox',
                    colors: ['black', 'white', 'gray', 'rgb(255,76,45)', 'rgb(123,227,118)', 'rgb(0,199,152)']
                    }
                    ],
                    tshirt_products_toshow: []
            }
        },
        created() {
            
        },
        mounted() {
            this.tshirt_products_toshow = this.tshirt_products;
        },
        methods: {
            filtered(values) {
                console.log(values);
                if(values.checkedBrands.length <= 0) {values.checkedBrands = this.categories[1].brands}
                if(values.checkedColors.length <= 0) {values.checkedColors = this.categories[2].colors}
                var filtered_tshirts = this.tshirt_products.filter((val) => {
                    return val.price <= values.max_price;
                });
                filtered_tshirts = filtered_tshirts.filter((val) => {
                    return values.checkedBrands.indexOf(val.brand) >= 0;
                });
                filtered_tshirts = filtered_tshirts.filter((val) => {
                    return values.checkedColors.indexOf(val.color) >= 0;
                });
                this.tshirt_products_toshow = filtered_tshirts;
            }
        }
    }
</script>

<style lang="scss" scoped>
@import "../assets/styles/reset.scss";
@import "../assets/styles/layout.scss";
.tshirtz{
  padding-top: 50px;
  main.content{
    overflow-y: scroll;
    padding: 20px;
    width: 76%;
    position: absolute;
    top: 50px;
    bottom: 22px;
    right: 0px;
    display: flex;
    flex-wrap: wrap;
    .tshirt_article{
        width: 250px;
        height: 300px;
        background: #fff;
        border: 1px solid #ddd;
        box-shadow: 0 0 15px rgba(0,0,0,.08), 0 0 4px rgba(0,0,0,.05);
        border-radius: 6px;
        font-weight: bold;
        position: relative;
        margin: 10px;
        h3{
            // float: left;
            position: absolute;
            top: 0;
            left: 0;
            text-transform: capitalize;
            width: 100%;
            text-align: left;
            padding: 5px;
            z-index: 1;
        }
        div.picture{
            display: block;
            position: relative;
            overflow: hidden;
            float: left;
            text-align: center;
            img{
                height: 300px;
            }
        }
        p{
            position: absolute;
            right: 5px;
            bottom: 5px;
            z-index: 1;
        }
    }
  }
}

</style>