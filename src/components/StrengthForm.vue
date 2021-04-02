<template>
  <div id="strengthFormContainer">
      <h2>Strength</h2>
      <form @submit.prevent="handleSubmit">
        <label>Date</label>
        <input 
        v-model="item.date"
        type="date"
        />

        <label>Exercise</label>
        <input 
        v-model="item.exercise"
        type="text"
        :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"
        />

        <label>Sets</label>
        <input 
        v-model="item.sets"
        type="number"
        :class="{'has-error' : submitting && invalidAmount}"
        @focus="clearStatus"
        />

        <label>Reps</label>
        <input 
        v-model="item.reps"
        type="number"
        :class="{'has-error' : submitting && invalidAmount}"
        @focus="clearStatus"
        />

        <label>Weight</label>
        <input 
        v-model="item.weight"
        type="number"
        :class="{'has-error' : submitting && invalidAmount}"
        @focus="clearStatus"
        />

        <button>Add Workout</button>

        <p v-if="error && submitting" class="errorMessage">❗️Please fill out all required fields</p>
        <p v-if="success" class="successMessage">✅ Workout sucessfully added</p>
      </form>
  </div>
</template>

<script>
export default {
    name: 'strength-form',
    data() {
        return {
            item: {
                date: '',
                exercise: '',
                sets: '',
                reps: '',
                weight: '',
            },
            submitting: false,
            error: false,
            success: false
        }
    },
    methods: {
        handleSubmit() {
            this.submitting = true;
            this.clearStatus()

            if(this.invalidItem || this.invalidAmount) {
                this.error = true
                return
            }

            this.$emit('add:item', this.item)
            this.item = {
                date: '',
                exercise: '',
                sets: '',
                reps: '',
                weight: '',
            }

            this.error = false
            this.success = true
            this.submitting = false

        },
        clearStatus() {
            this.success = false
            this.error = false
        }
    },
    computed: {
        invalidItem() {
            return this.item.exercise.trim() === ''
        },
        invalidAmount() {
            return this.item.sets === '' || this.item.reps === '' || this.item.weight === ''
        },
    }
}
</script>

<style>
#strengthFormContainer h2 {
    margin: 2rem 0 0 0;
}
form {
        margin-bottom: 3rem;
    }
    [class*='-message'] {
        font-weight: 500;
    }
    .errorMessage {
        color: #d33c40;
    }
    .successMessage {
        color: #32a95d;
    }
</style>