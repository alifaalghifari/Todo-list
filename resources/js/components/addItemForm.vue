<template>
  <div class="flex justify-center items-center space-x-2">
    <input
      type="text"
      v-model="item.name"
      class="w-full outline-none h-6 px-3 rounded ring-1 ring-gray-400 focus:ring-blue-300 text-sm text-gray-400 duration-150"
    />
    <div
      :class="[ item.name ? 'bg-opacity-100 cursor-pointer text-white' :'bg-opacity-0 text-gray-600' , 'bg-green-600 rounded-full  transition-all duration-150']"
      v-on:click="addItem"
    >
      <svg
        class="h-6 w-6   "
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M12 6v6m0 0v6m0-6h6m-6 0H6"
        />
      </svg>
    </div>

  </div>
</template>

<script>
export default {
  data: function () {
    return {
      item: {
        name: "",
      },
    };
  },
  methods: {
    addItem: function () {
      if (this.item.name == "") {
        return;
      }

      axios
        .post("api/item/store", {
          item: this.item,
        })
        .then((response) => {
          if (response.status == 201) {
            this.item.name = "";
            this.$emit("reloadlist");
            swal("Berhasil!", "Data berhasil ditambahakan!", "success");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>