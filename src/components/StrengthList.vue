<template>
  <div id="strengthHistoryContainer">
      <h4>Strength</h4>
      <table>
          <thead>
              <tr>
                  <th>Date</th>
                  <th>Exercise</th>
                  <th>Sets</th>
                  <th>Reps</th>
                  <th>Weight</th>
                  <th>Actions</th>
              </tr>
          </thead>
          <tbody>
            <tr v-for="item in items" :key="item.id">
                <td>{{item.date}}</td>
                <td>{{item.exercise}}</td>
                <td>{{item.sets}}</td>
                <td>{{item.reps}}</td>
                <td>{{item.weight}}</td>
                <td><button @click="$emit('delete:item', item.id)">Delete</button></td>
            </tr>
          </tbody>
      </table>
      
  </div>
</template>

<script>
export default {
    name: 'StrengthList',
    props: {
        items: Array
    }
}
</script>

<style>

</style>