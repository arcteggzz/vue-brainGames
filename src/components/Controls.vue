<template>
    <main class="flex flex-col justify-center items-center py-8 space-y-8 h-[30vh]">
        <h1 class="text-[2.25rem] font-[700] text-[#101828] leading-[60px]">Brain Games</h1>
        <p class="text-[1.25rem] font-[400] text-[#667085] leading-[30px]">Pick the cards in the correct order</p>
        <section class="flex space-x-6">
            <div class="flex space-x-6">
                <button :class="buttonStyle" @click="startGame">Start</button>
                <button :class="buttonStyle" @click="endGame">End</button>
            </div>
            <div class="flex space-x-6">
                <h2 :class="infoStyle">Level: 0</h2>
                <h2 :class="infoStyle">Time: {{ timeSpentText }}</h2>
            </div>
        </section>
    </main>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
    name: 'Controls',
    components: {},
    computed: {
        gameActive(){
            return this.$store.state.gameActive;
        }
    },
    data () {
        return {
            buttonStyle: `text-white font-[500] text-[1rem] bg-[#7F56D9] rounded-[0.5rem] px-[2rem] py-[0.85rem]`,
            infoStyle: `text-[1.2rem] font-[500] text-[#6941C6] leading-[1.5rem] py-[1rem] w-[10rem] bg-[#F9F5FF] rounded-[1rem] text-center`,
            timeSpentText: "00:00",
            timeSpentNum: 0,
        }
    },
    methods: {
        startGame() {
            this.$store.state.gameActive = true;
            setInterval(()=>{
                if (this.$store.state.gameActive){
                    this.timeSpentNum++;
                    const divisor_for_minutes = this.timeSpentNum % (60 * 60);
                    const minutes = Math.floor(divisor_for_minutes / 60);

                    const divisor_for_seconds = divisor_for_minutes % 60;
                    const seconds = Math.ceil(divisor_for_seconds);

                    this.timeSpentText = `${minutes}:${seconds}`
                }
            }, 1000);
        },
        endGame() {
            this.$store.state.gameActive = false;
            this.timeSpentNum = 0;
            this.timeSpentText = `00:00`;
        }
    }
});
</script>

<style>
</style>
