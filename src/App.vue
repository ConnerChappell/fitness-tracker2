<template>
  <div id="app" class="small-container">
    <h1>Fitness Tracker</h1>

    <p id="selectStatement">Please select the type of workout you would like to add</p>
    <button v-on:click="toggle = true">Strength</button>
    <button v-on:click="toggle = false">Endurance</button>

    <div v-if="toggle">
      <strength-form 
      @add:item="addStrength"
      @add:workoutType="strengthHistory"
      />
    </div>
    <div v-else>
      <endurance-form 
      @add:item="addEndurance"
      />
    </div>

    <div class="workoutHistory">
      <h2>Workout History</h2>

      <strength-list
      :items="strengthHistory"
      @delete:item="deleteStrength"
      />

      <endurance-list 
      :items="enduranceHistory"
      @delete:item="deleteEndurance"
      />
    </div>
  </div>
</template>

<script>
import EnduranceForm from './components/EnduranceForm.vue';
import EnduranceList from './components/EnduranceList.vue';
import StrengthForm from './components/StrengthForm.vue';
import StrengthList from './components/StrengthList.vue';


export default {
  name: 'App',
  components: {
    StrengthList,
    StrengthForm,
    EnduranceList,
    EnduranceForm
  },
  data() {
    return {
      toggle: true,
      strengthHistory: [
        {
          id: 1,
          exercise: 'Dumbbell Curls',
          sets: 3,
          reps: 10,
          weight: 30,
          date: '2021-3-20'
        },
        {
          id: 2,
          exercise: 'Bench Press',
          sets: 3,
          reps: 10,
          weight: 200,
          date: '2021-3-21'
        },
      ],
      enduranceHistory: [
        {
          id: 1,
          exercise: 'Run',
          distance: '3 miles',
          duration: '20 minutes',
          date: '2021-3-18'
        },
        {
          id: 2,
          exercise: 'Swim',
          distance: '10 laps',
          duration: '15 minutes',
          date: '2021-3-19'
        },
      ],
    };
  },
  methods: {
    addEndurance(item) {
      const lastId = this.enduranceHistory.length > 0
      ? this.enduranceHistory[this.enduranceHistory.length - 1].id : 0

      const id = lastId + 1

      const newEndurance = {...item, id}

      this.enduranceHistory = [...this.enduranceHistory, newEndurance]
    },
    addStrength(item) {
      const lastId = this.strengthHistory.length > 0
      ? this.strengthHistory[this.strengthHistory.length - 1].id : 0

      const id = lastId + 1

      const newStrength = {...item, id}

      this.strengthHistory = [...this.strengthHistory, newStrength]
    },
    deleteStrength(id) {
      this.strengthHistory = this.strengthHistory.filter(item => item.id !== id)
    },
    deleteEndurance(id) {
      this.enduranceHistory = this.enduranceHistory.filter(item => item.id !== id)
    }
  }
}
</script>

<style>
h1 {
    font-size: 75px;
  }
  h2 {
    margin-bottom: .75rem;
    padding-bottom: .5rem;
    /* border-bottom: 1px solid #000; */
  }
  h4 {
    margin-top: 0;
  }
  #selectStatement {
    margin-bottom: 0;
  }
  button {
    background: #000;
    border: 1px solid #000;
    margin: .5rem .5rem .5rem 0;
    transition: all .4s;
  }
  button:hover {
    background: #fff;
    border: 1px solid #000;
    color: #000;
  }
  button:focus {
    background: #fff;
    color: #000;
    border: 1px solid #000;
    outline: none;
  }
  .small-container {
    max-width: 680px;
  }
</style>
