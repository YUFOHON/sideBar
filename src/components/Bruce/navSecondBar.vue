<template>
  <div class="container-md">
    <nav class="navbar navbar-expand-lg bg-body-tertiary d-flex justify-content-between ">
      <div class="container-flex ">

        <a v-for="a in props.arr" :key="a.name" :href=a.URL>{{ a.name }}/</a>
        <!-- class="navbar-brand text-danger" -->
      </div>

      <div class="d-flex-button">

        <button v-if="props.sortButton" type="button" class="btn btn-primary dropdown-toggle" data-bs-toggle="dropdown"
          aria-expanded="false">
          Sort
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" v-on:click="this.$emit('sorting','Ascending')" >Date Ascending</a></li>
            <li><a class="dropdown-item" v-on:click="this.$emit('sorting','Descending')">Date Descending</a></li>
            <li>
              <hr class="dropdown-divider">
            </li>
            <li><a class="dropdown-item" href="#">Head</a></li>
          </ul>
        </button>

        <button v-if="props.eventHistoryButton" type="button" class="btn btn-secondary">Event History</button>
        <button v-if="props.addButton" type="button" class="btn btn-success">Add</button>



      </div>


      <form v-if="props.search" class="d-flex" role="search">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
    </nav>

  </div>
</template>

<script>
// import { ref } from 'vue'

export default {
  name: 'navSecondBar',
  props: {
    arr: Array,
    sortButton: { Boolean, default: false },
    eventHistoryButton: { Boolean, default: false },
    addButton: { Boolean, default: false },
    search: { Boolean, default: false },
  },
  setup(props) {

    return {
      props
    }

  }
}
</script>

<style scoped>
.container-md {
  max-width: 90%;
  border-radius: 20px;
  background-color: #c1c1c153;
}


.navbar-brand {
  color: rgb(221, 10, 10);
  font-size: 2rem;
  margin-right: 5px;
}

.d-flex-button {
  position: relative;
  display: flex;
  justify-content: space-between;
  width: 25%;
  margin-left: 28%;
}

.dropdown-menu {

  /* background-color: #c1c1c153; */

}

.dropdown-item:hover {
  background-color: #99e7f7d3;
}

a {
  color: #000000ef;
  text-decoration: none;
  /* size of text increse */
  font-size: 1.2rem;

}

a:hover {
  background-color: #99e7f7d3;
  border-radius: 10px;
}
</style>