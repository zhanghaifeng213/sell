<template>
    <div class="countcontrol">
        <div class="cartcontrol">
            <transition>
                <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart">
                    <span class="inner inner1 icon-remove_circle_outline"></span>
                </div>
            </transition>
            <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
            <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
        </div>
    </div>
</template>

<script type="text/ecmascript-6">
    import Vue from 'vue';
    export default {
        props: {
            food: {
                type: Object
            }
        },
        methods: {
            addCart(event) {
                if (!event._constructed) {
                    return;
                };
                if (!this.food.count) {
                    Vue.set(this.food, 'count', 1);
                } else {
                    this.food.count++;
                }
            },
            decreaseCart(event) {
                if (!event._constructed) {
                    return;
                };
                if (this.food.count) {
                    this.food.count--;
                }
            }
        }
    };
</script>

<style lang="stylus" rel="stylesheet/stylus">
    @import "cartcontrol.styl"
</style>