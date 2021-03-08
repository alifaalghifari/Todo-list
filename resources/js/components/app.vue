<template>
  <div class="w-80 m-auto rounded-lg mt-5">
    <div class="bg-gray-300 p-5 ">
      <h2 class="text-center text-xl mb-5">Todo List</h2>
      <add-item-form v-on:reloadlist="getItems()" />
    </div>
    <list-view
      :items="items"
      v-on:reloadlist="getItems()"
    />
  </div>
</template>

<script>
import addItemForm from "./addItemForm";
import listView from "./listView";

export default {
  data: function () {
    return {
      items: [],
    };
  },
  components: {
    addItemForm,
    listView,
  },
  methods: {
    getItems: function () {
      axios
        .get("api/items")
        .then((response) => {
          if (typeof response.data != "string") this.items = response.data;
        })
        .catch((error) => {
          alert(error);
        });
    },
  },
  created() {
    this.getItems();
  },
};
</script>