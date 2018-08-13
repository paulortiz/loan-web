<template>
    <div id="app">
        <h1>Calculate your desired loan</h1>
        <div class="wrapper">
            <Slider 
                title="How much would you like to loan?" 
                ref="amountSlider"
                :min="25000"               
                :max="100000"
                minDisplay="S$ 25,000"
                maxDisplay="S$ 100,000"/>

            <Slider
                title="What is your preferred tenor?" 
                ref="tenorSlider"
                :min="1"               
                :max="24"
                minDisplay="1 month"
                maxDisplay="24 months"/>

            <button name="calculate" v-on:click="getRepayment"> Calculate </button>       
        </div>          
        <div class="breaker">&nbsp;</div>
        <div>
            <h2>Computed Repayment</h2>
            <div class="wrapper">
                <div class="computed-repayment">
                    <ResultItem title="Original Principal" v-bind:value="repayment.originalPrincipal | amount" />                    
                    <ResultItem title="Monthly Installment" v-bind:value="repayment.monthly | amount" />
                    <ResultItem title="Interest Rate" v-bind:value="repayment.interest | percent" />
                    <ResultItem title="Interest Amount" v-bind:value="repayment.interestAmount | amount" />
                    <ResultItem title="Ending Principal" v-bind:value="repayment.endingPrincipal | amount" />
                </div>            
            </div>
        </div>
    </div>
</template>

<script>
//imports
import Slider from './components/slider/Slider.vue'
import ResultItem from './components/ResultItem.vue'
import axios from 'axios'

export default {
    name: 'app',
    components: {
        Slider,
        ResultItem
    },
    data: function() {
        return {
            repayment: {}
        }
    },
    methods : {
        getRepayment: function() {
            let loanAmount = this.$refs.amountSlider.sliderValue;
            let tenor = this.$refs.tenorSlider.sliderValue
            const baseURL = "http://localhost:3000"
            const headers = { 'amount': loanAmount, 'tenure': tenor }
            
            if (loanAmount < 25000 || loanAmount > 100000) {
                alert("Please choose amount between 25,000 to 100,000")
                return
            }

            if (tenor < 1 || tenor > 24) {
                alert("Please choose tenor between 1 to 24")
                return
            }
            
            axios.get(`${baseURL}/repayment`, { headers }).then(response => {
                console.log("===>>>", response.data)
                let data = response.data;
                let error = data.error;
                this.repayment = data.body;
            }).catch(e => {
                console.error(`Failed to get response error : ${e}`)
            })
        }
    },
    filters: {
        amount : function(value) {
            if (!value) return ''
            value = parseFloat(value).toFixed(2)
            return Number(value).toLocaleString('en');
        },

        percent : function(value) {
            if (!value) return ''
            return `${value}%`
        }
    }
}
</script>

<style src="./Style.css"></style>
