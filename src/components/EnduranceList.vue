<template>
  <div id="enduranceHistoryContainer">
      <h4>Endurance</h4>
      <table>
          <thead>
              <tr>
                  <th>Date</th>
                  <th>Exercise</th>
                  <th>Distance</th>
                  <th>Duration</th>
                  <th>Actions</th>
              </tr>
          </thead>
          <tbody>
            <tr v-for="item in items" :key="item.id">
                <td>{{item.date}}</td>
                <td>{{item.exercise}}</td>
                <td>{{item.distance}}</td>
                <td>{{item.duration}}</td>
                <td><button @click="$emit('delete:item', item.id)">Delete</button></td>
            </tr>
          </tbody>
      </table>
      
  </div>
</template>

<script>
export default {
    name: "EnduranceList",
    props: {
        items: Array
    }
}
</script>

<style>

</style>