<template>
  <div id="strengthFormContainer">
      <h2>Endurance</h2>
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

        <label>Distance</label>
        <input 
        v-model="item.distance"
        type="text"
        :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"
        />

        <label>Duration</label>
        <input 
        v-model="item.duration"
        type="text"
        :class="{'has-error' : submitting && invalidItem}"
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
    name: 'endurance-form',
    data() {
        return {
            item: {
                date: '',
                exercise: '',
                distance: '',
                duration: '',
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
                distance: '',
                duration: '',
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
            return this.item.exercise.trim() === '' || this.item.distance.trim() === '' || this.item.duration.trim() === ''
        },
    }
}
</script>

<style>

</style>