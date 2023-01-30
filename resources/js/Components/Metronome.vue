<script>
    export default {
        name: "Metronome",
        data() {
            return {
                tempo:140,
                minTempo:20,
                maxTempo:280,
                beatsPerMeasure:4,
                minBeatsPerMeasure:1,
                maxBeatsPerMeasure:8,
                tempoDescription:"mid-tempo"
            }
        },
        methods: {
            updateTempo(event) {
                this.tempo = event.target.value;
                this.updateTempoDescription();
            },
            decreaseTempo() {
                if (this.tempo > this.minTempo) {
                    this.tempo--;
                    this.updateTempoDescription();
                }
            },
            increaseTempo() {
                if (this.tempo < this.maxTempo) {
                    this.tempo++;
                    this.updateTempoDescription();
                }
            },
            decreaseBeatsPerMeasure() {
                if (this.beatsPerMeasure > this.minBeatsPerMeasure) {
                    this.beatsPerMeasure--;
                }
            },
            increaseBeatsPerMeasure() {
                if (this.beatsPerMeasure < this.maxBeatsPerMeasure) {
                    this.beatsPerMeasure++;
                }
            },
            updateTempoDescription() {
                if (this.tempo > 220 && this.tempo <= 280) {
                    this.tempoDescription = 'hypertone';
                    return;
                }
                if (this.tempo <= 220 && this.tempo > 200) {
                    this.tempoDescription = 'super-fast';
                    return;
                }
                if (this.tempo <= 200 && this.tempo > 170) {
                    this.tempoDescription = 'fast';
                    return;
                }
                if (this.tempo <= 170 && this.tempo >= 140) {
                    this.tempoDescription = 'mid-tempo';
                    return;
                }
                if (this.tempo < 140 && this.tempo > 100) {
                    this.tempoDescription = 'groovie';
                    return;
                }
                if (this.tempo <= 100 && this.tempo > 60) {
                    this.tempoDescription = 'slowpoke';
                    return;
                }
                if (this.tempo <= 60 && this.tempo > 40) {
                    this.tempoDescription = 'drone, ambient';
                    return;
                }
                if (this.tempo <= 40 && this.tempo >= 20) {
                    this.tempoDescription = 'almost dead';
                }
            },
        }
    }
</script>

<template>
<div class="container">
    <div class="metronome">
        <div class="bpm-display">
            <span class="tempo">{{ tempo }}</span>
            <span class="bpm">BPM</span>
        </div>
        <div class="tempo-text">{{ tempoDescription }}</div>
        <div class="tempo-settings">
            <div class="adjust-tempo-btn decrease-tempo" v-on:click="decreaseTempo">-</div>
            <input type="range" min="20" max="280" step="1" class="tempo-slider" v-bind:value="tempo" v-on:input="updateTempo"/>
            <div class="adjust-tempo-btn increase-tempo" v-on:click="increaseTempo">+</div>
        </div>
        <div class="start-stop">START</div>
        <div class="measures">
            <div class="subtract-beats stepper" v-on:click="decreaseBeatsPerMeasure">-</div>
            <div class="measure-count">{{ beatsPerMeasure }}</div>
            <div class="add-beats stepper" v-on:click="increaseBeatsPerMeasure">+</div>
        </div>
        <span class="beats-per-measure">Beats per measure</span>
    </div>
</div>
</template>

<style scoped>
    .container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 20vh;
    }
    .metronome {
        display: flex;
        flex-direction: column;
        width: 300px;
        height: 250px;
        justify-content: space-between;
        -webkit-user-select: none; /* Safari */
        -moz-user-select: none; /* Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
        user-select: none; /* Standard */
    }
    .bpm-display {
        width: 100%;
        text-align: center;
        color: var(--nice-red);
        font-weight: bold;
    }
    .bpm-display .tempo {
        font-size: 4em;
    }
    .tempo-text {
        font-size: .8em;
        text-transform: uppercase;
        text-align: center;
    }
    .tempo-settings {
        display: flex;
        justify-content: space-between;
    }
    .tempo-settings .adjust-tempo-btn {
        width: 30px;
        height: 30px;
        font-size: 30px;
        border-radius: 50%;
        border: 1px solid var(--nice-white);
        text-align: center;
        cursor: pointer;
    }
    .tempo-settings .adjust-tempo-btn:hover {
        background: var(--nice-red);
        color: var(--nice-white);
    }
    .tempo-settings .decrease-tempo {
        line-height: 27px;
    }
    .tempo-settings .increase-tempo {
        line-height: 27px;
    }
    input[type=range] {
        -webkit-appearance: none;
        background-color: transparent;
        width: 70%;
    }
    input[type=range]::-webkit-slider-thumb {
        -webkit-appearance: none;
    }
    input[type=range]:focus {
        outline: none;
    }
    input[type=range]::-webkit-slider-thumb {
        -webkit-appearance: none;
        width: 16px;
        height: 16px;
        border-radius: 50%;
        background: var(--nice-pinkie);
        cursor: pointer;
        margin-top: -8px;
    }
    input[type=range]::-moz-range-thumb {
        -webkit-appearance: none;
        width: 16px;
        height: 16px;
        border-radius: 50%;
        background: var(--nice-pinkie);
        border: none;
    }
    input[type=range]::-webkit-slider-runnable-track {
        width: 100%;
        height: 1px;
        background: var(--nice-white);
    }
    input[type=range]::-moz-range-track {
        width: 100%;
        height: 1px;
        background: var(--nice-white);
    }
    .start-stop {
        width: 50px;
        height: 50px;
        font-size: 0.7em;
        text-align: center;
        background-color: var(--nice-red);
        border-radius: 50px;
        color: white;
        line-height: 50px;
        margin: 0 auto;
        cursor: pointer;
    }
    .start-stop:hover {
        background: var(--nice-pinkie);
    }
    .measures {
        /*display: none;*/
        display: flex;
        justify-content: center;
    }
    .measures .stepper {
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: none;
        text-align: center;
        margin: 0 5px;
        cursor: pointer;
    }
    .measures .stepper:hover {
        background: var(--nice-pinkie);
        color: white;
    }
    .measures .add-beats {
        line-height: 18px;
    }
    .measures .subtract-beats {
        line-height: 20px;
    }
    .beats-per-measure {
        text-align: center;
        font-size: .5em;
        text-transform: uppercase;
    }
</style>
