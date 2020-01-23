<template>
    <div class="container">
        <div class="card mt-5">
            <h2 class="card-header" style="text-align: center;">Laser Cutter Queue</h2>

            <!-- Displays the current queue count -->
            <div class="m-3" v-cloak v-if="numPeople == 1">
                <p>There is {{ numPeople }} person in the queue</p>
            </div>
            <div class="m-3" v-cloak v-if="numPeople > 1">
                <p>There are {{ numPeople }} people in the queue</p>
            </div>

            <!-- Displays sign-up form -->
            <form v-cloak class="m-3">
                <div class="form-row">
                    <div class="col">
                        <input type="text" v-model="firstName" placeholder="First Name" />
                    </div>
                    <div class="col">
                        <input type="text" v-model="lastName" placeholder="Last Name" />
                    </div>
                    <div class="col">
                        <button type="button" @click="addPerson(firstName, lastName)" class="btn">Add</button>
                    </div>
                </div>
            </form>

            <!-- Displays table that holds the queue-->
            <table class="table">
                <thead class="thead-light">
                    <th>#</th>
                    <th>Name</th>
                    <th>Time-In</th>
                    <th>Checks</th>
                    <th>Remove</th>
                </thead>

                <!-- Displays the current queue -->
                <tbody>
                    <tr v-for="(p, index) in people" :key="index">
                        <td>{{ index + 1 }}</td>
                        <td>{{ getName(index) }}</td>
                        <td>{{ getTime(index) }}</td>
                        <td>
                            <input type="checkbox" id="checkOne" />
                            <label for="checkOne">#1</label>
                            <input type="checkbox" id="checkTwo" />
                            <label for="checkTwo">#2</label>
                            <input type="checkbox" id="checkThree" />
                            <label for="checkThree">#3</label>
                        </td>
                        <td>
                            <button type="button" @click="remove(index)" class="btn btn-warning">remove</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
    export default {
        name: "LaserQueue",
        props: {
            people: Array,
            times: Array
        },
        computed: {
            // Calculates number of people in queue
            numPeople: function () {
                return this.people.length;
            }
        },
        methods: {
            // Add name and check-in time to the queue
            addPerson: function (first, last) {
                var today = new Date();
                this.times[this.times.length] = today.getHours() + ":" + today.getMinutes() + ":" + today
                    .getSeconds();
                this.people[this.people.length] = first + " " + last;
                this.people.splice();
            },
            // Returns the name at a certain index
            getName: function (index) {
                return this.people[index];
            },
            // Returns time at a certain index
            getTime: function (index) {
                return this.times[index];
            },
            // Removes person and time from the data
            remove: function (index) {
                this.people.splice(index, 1);
                this.times.splice(index, 1);
            }
        }
    };
</script>