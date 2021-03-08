<template>
  <div class="flex items-center">
    <div class="flex flex-auto items-center space-x-6">
      <input
        type="checkbox"
        v-model="item.completed"
        @change="updateCheck()"
        class="border-0"
      >
      <span :class="[item.completed ? 'line-through' : '','w-full text-gray-500 text-sm font-normal leading-relaxed']">{{ item.name }}</span>
    </div>
    <button
      v-on:click="removeItem()"
      class="justify-self-end flex-none focus:outline-none"
    >
      <svg
        class="h-5 w-5 text-red-400"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
        />
      </svg>
    </button>
  </div>

</template>

<script>
export default {
  props: ["item"],
  methods: {
    updateCheck: function () {
      axios
        .put("api/item/" + this.item.id, {
          item: this.item,
        })
        .then((response) => {
          if (response.status == 200) {
            this.$emit("itemchanged");
          }
        })
        .catch((error) => {
          alert(error);
        });
    },
    removeItem: function () {
      axios
        .delete("api/item/" + this.item.id)
        .then((response) => {
          if (response.status == 200) {
            this.$emit("itemchanged");
            swal("Berhasil!", "Data berhasil dihapus!", "success");
          }
        })
        .catch((error) => {
          alert(error);
        });
    },
  },
};
</script>