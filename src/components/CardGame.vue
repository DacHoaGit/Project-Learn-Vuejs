<template>
    <div class="card">
        <div class="card__inner" :class="{'is-flipped': isFlipped}" @click="onToggleFlipCard">
            <div class="card__face card__face--front">
                <div class="card__content">
                </div>
            </div>
            <div class="card__face card__face--back">
                <div class="card__content" :style="{backgroundImage: `url(${require('@/assets/'+ imgBackFaceUrl)})`}">
                </div>
            </div>
        </div>
    </div>
</template>

<style>
    .card {
        display: inline-block;
        margin-right: 1rem;
        margin-bottom: 1rem;
        width: 90px;
        height: 120px;
    }
    .card__inner {
        width: 100%;
        height: 100%;
        transition: transform 1s;
        transform-style: preserve-3d;
        cursor: pointer;
        position: relative;
        
    }
    .card__inner.is-flipped{
        transform: rotateY(-180deg);
    }


    .card__face {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
        overflow: hidden;/*  child khong tran ra ngoai */
        border-radius: 1rem;
        padding: 1rem;
        box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
    }

    .card__face--front .card__content{
        background: url("../assets/images/icon_back.png") no-repeat center center;
        background-size: 40px 40px;
        height: 100px;
        widows: 100px;
    }

    .card__face--back{
        background-color: var(--light);
        transform: rotateY(-180deg);

    }
    .card__face--back .card__content{
        background-size: contain;
        background-position: center center;
        background-repeat: no-repeat;
        height: 100px;
        widows: 100px;
    }
</style>

<script>
export default {

    props: {
        imgBackFaceUrl: {
            type:[Array,String],
            default: function(){
                return [];
            }
        },
        card:{
            type: [String,Number,Array,Object], 
        }

    },
    data() {
        return {
            isFlipped:false,
        };
    },
    methods: {
        onToggleFlipCard(){
            this.isFlipped = !this.isFlipped;
            if(this.isFlipped)
                this.$emit("onFlip",this.card);
        },
        onFlipBackCard(){
            console.log(1221);
            
            this.isFlipped = false;
        }
    },
}
</script>