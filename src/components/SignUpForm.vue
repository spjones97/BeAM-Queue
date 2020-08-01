<template>
  <div class="signcontainer">
    <form v-cloak class="m-3">
      <div class="form-row">
        <div class="col">
          <input class="firstin" type="text" v-model="firstName" placeholder="First Name" />
        </div>
        <div class="col">
          <input class="lastin" type="text" v-model="lastName" placeholder="Last Name" />
        </div>
        <div class="col">
          <button
            class="btn"
            type="button"
            @click="addToQueue(firstName, lastName)"
            id="queuebtn"
          >ADD</button>
        </div>
      </div>
    </form>
  </div>
</template>