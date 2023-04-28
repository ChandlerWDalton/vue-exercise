<template>
  <div class="hello">
    <h1>We go Gym</h1>
    <div class="body">
      <div class="add">
        <div class="new-workout">
          <h2>New Workout</h2>
          <label for="date">Date</label>
          <input type="date" id="date" v-model="newWorkout.date" />
          <table>
              <tr>
                <th>Excercise</th>
                <th>Sets</th>
                <th>Reps</th>
                <th>Weight</th>
                <th>Distance</th>
                <th>Time</th>
              </tr>
              <tr v-for="excercise in newWorkout.excercises" :key="excercise.name">
                <td>{{ excercise.name}}</td>
                <td>{{ excercise.sets != 0 ? excercise.sets : '-' }}</td>
                <td>{{ excercise.reps  != 0 ? excercise.reps : '-' }}</td>
                <td>{{ excercise.weight != 0 ? excercise.weight : '-' }}</td>
                <td>{{ excercise.distance != 0 ? excercise.distance : '-' }}</td>
                <td>{{ excercise.time != 0 ? excercise.time : '-' }}</td>
              </tr>
          </table>
          <button v-if="!showNewExcercise" @click="showNewExcercise = true">Add Excercise</button>
          <button :disabled="!newWorkout.date || newWorkout.excercises.length < 1" @click="submit">Add Workout</button>
        </div>
        <div v-if="showNewExcercise" class="new-excercise">
          <h2>New Excercise</h2>
          <label for="name">Name</label>
          <input type="text" id="name" v-model="newExcercise.name" />
          <div>Type
            <button @click="cardio = false" >Strength</button>
            <button @click="cardio = true" >Cardio</button>
          </div>
          <label v-if="!cardio" for="sets">Sets</label>
          <input v-if="!cardio" type="number" id="sets" v-model="newExcercise.sets" />
          <label v-if="!cardio" for="reps">Reps</label>
          <input v-if="!cardio" type="number" id="reps" v-model="newExcercise.reps" />
          <label v-if="!cardio" for="weight">Weight</label>
          <input v-if="!cardio" type="number" id="weight" v-model="newExcercise.weight" />
          <label v-if="cardio" for="distance">Distance</label>
          <input v-if="cardio" type="number" id="distance" v-model="newExcercise.distance" />
          <label v-if="cardio" for="time">Time</label>
          <input v-if="cardio" type="number" id="time" v-model="newExcercise.time" />
          <button @click="submitExercise">Add to Workout</button>
          <button @click="cancelAdd">Cancel</button>
        </div>

      </div>
      <div class="history">
        <h2>History</h2>
        <ul>
          <li v-for="workout in history" :key="workout.date">
            <h4>{{ workout.date }}</h4>
            <table>
              <tr>
                <th>Excercise</th>
                <th>Sets</th>
                <th>Reps</th>
                <th>Weight</th>
                <th>Distance</th>
                <th>Time</th>
              </tr>
              <tr v-for="excercise in workout.excercises" :key="excercise.name">
                <td>{{ excercise.name}}</td>
                <td>{{ excercise.sets != 0 ? excercise.sets : '-' }}</td>
                <td>{{ excercise.reps  != 0 ? excercise.reps : '-' }}</td>
                <td>{{ excercise.weight != 0 ? excercise.weight : '-' }}</td>
                <td>{{ excercise.distance != 0 ? excercise.distance : '-' }}</td>
                <td>{{ excercise.time != 0 ? excercise.time : '-' }}</td>
              </tr>
          </table>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data() {
    return {
      history: [],
      newWorkout: {
        date: "",
        excercises: [],
      },
      newExcercise: {
        name: "",
        sets: 0,
        reps: 0,
        weight: 0,
        distance: 0,
        time: 0,
      },
      showNewExcercise: false,
      cardio: false
    };
  },

  methods: {
    submitExercise() {
      this.newWorkout.excercises.push(this.newExcercise);
      this.newExcercise = {
        name: "",
        sets: 0,
        reps: 0,
        weight: 0,
        distance: 0,
        time: 0
      };
      this.showNewExcercise = false;
    },

    submit() {
      this.history = [this.newWorkout, ...this.history]
      this.newWorkout = {
        date: "",
        excercises: [],
      };
    },

    cancelAdd() {
      this.showNewExcercise = false;
      this.newExcercise = {
        name: "",
        sets: 0,
        reps: 0,
        weight: 0,
        distance: 0,
        time: 0
      };
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.add {
  display: flex;
  flex-direction: row;
  justify-content: center;
  border-bottom: 3px solid black;
}

.new-workout {
  margin: 1em;
  display: flex;
  flex-direction: column;
  width: 500px;
}

.new-excercise {
  margin: 1em;
  display: flex;
  flex-direction: column;
  width: 200px;
}

.history li {
  margin: 1em;
  border: 2px solid black;
  border-radius: 5px;
}

table {
  border-collapse: collapse;
  padding: .5em;
}

.history li h4{
  padding: 1em;
  background-color: #8ca1ff;
}

button {
  margin: .5em;
  padding: 0.5em;
  border-radius: 5px;
  border: 1px solid black;
  background-color: #8ca1ff;
}

input {
  margin: .5em;
  padding: 0.5em;
  border-radius: 5px;
  border: 1px solid black;
  text-align: left;
}

th {
  padding: .5em;
}

td {
  padding: .5em;
  text-align: center;
}

tr {
  border: 2px solid black;
  border-collapse: collapse;
}

h1 {
  border-bottom: 3px solid black;
  padding-bottom: 2em;
}

</style>
