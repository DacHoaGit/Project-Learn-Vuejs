<template>
    <div class="screen">
        <h1>InteractScreen component</h1>
        <cardFlip v-for="(card,index) in cardsContext" 
            :key="index" 
            :imgBackFaceUrl="`images/${card}.png`"
            :card="{index:index,value:card}"
            :ref="`card${index}`"
            @onFlip="checkRule($event)"
        />
    </div>
</template>


<script>
import cardFlip from "./CardGame.vue"
export default {
    props:{
        cardsContext: {
            type: Array,
            default: function(){
                return [];
            },
        }
    },
    components: {
        cardFlip,
    },
    data(){
        return {
            rules: [],

        }
    },
    methods: {
        checkRule(card){
            if(this.rules.lenght === 2){
                return false;
            }
                
            this.rules.push(card);
            if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value){
                console.log(1);
            }
            else if (this.rules.length === 2 && this.rules[0].value !== this.rules[1].value){
                setTimeout(()=>{
                    this.$refs.card-(this.rules[0].index).onFlipBackCard();
                    this.$refs.card-(this.rules[1].index).onFlipBackCard();
                    this.rules = [];
                },800);
                

            }
            else
                return false;
        }
    }
}
</script>