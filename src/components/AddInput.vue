<template>
  <div>
    <v-card class="mx-auto px-4 py-4 my-10" max-width="344">
      <v-card-text>
        <v-text-field
          density="compact"
          variant="solo"
          label="Search"
          append-inner-icon="mdi-magnify"
          single-line
          v-model="search"
        ></v-text-field>

        <v-text-field
          density="compact"
          variant="solo"
          label="What need to add"
          single-line
          v-model.trim="userInput"
        ></v-text-field>
        <v-text class="invalid" v-if="!isValid"
          >Please Add Something...!</v-text
        >
        <v-btn
          block
          color="success"
          size="large"
          type="submit"
          variant="elevated"
          @click="addToList"
        >
          ADD
        </v-btn>
      </v-card-text>
    </v-card>
    <v-divider></v-divider>
    <v-list-item
      class="tile"
      v-for="(todo, index) in filteredSearch"
      :key="index"
      :value="todo"
      :title="todo"
    >
      <template v-slot:append>
        <v-btn color="red" @click="deleteItem(index)" variant="text"
          >Delete</v-btn
        >
        <v-btn color="success" @click="editItem(index)" variant="text"
          >Edit</v-btn
        >
      </template>
    </v-list-item>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userInput: "",
      todos: [],
      edit: null,
      search: "",
      isValid: true,
    };
  },
  computed: {
    filteredSearch() {
      return this.todos.filter((item) => {
        return item.toLowerCase().includes(this.search.toLowerCase());
      });
    },
    colorchange(index) {
      return index % 2 === 0 ? "bg-bisque" : "bg-darksalmon";
    },
  },
  methods: {
    addToList() {
      if (this.userInput === "") {
        this.isValid = false;
        return;
      }
      if (this.edit === null) {
        this.todos.push(this.userInput);
        this.userInput = "";
      } else {
        this.todos[this.edit] = this.userInput;
        this.edit = null;
        this.userInput = "";
      }
    },
    deleteItem(index) {
      this.todos.splice(index, 1);
    },
    editItem(ind) {
      this.userInput = this.todos[ind];
      this.edit = this.userInput;
      this.todos.filter((ele) => {
        if (this.todos.indexOf(ele) === ind) {
          this.userInput = ele;
        }
      });
      this.edit = ind;
    },
  },
};
</script>

<style scoped>
.invalid {
  color: red;
}
.tile:nth-last-child(even) {
  background-color: darkgray;
  color: bisque;
}
.tile:nth-last-child(odd) {
  background-color: whitesmoke;
  color: black;
}

.tile:hover {
  background-color: #333;
  color: #fff;
  cursor: pointer;
}

</style>
