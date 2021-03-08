<template>
  <div class="">
    <div v-if="items.length">
      <div
        v-for="(item, index) in items"
        :key="index"
      >
        <list-item
          :item="item"
          v-on:itemchanged="$emit('reloadlist')"
          class="bg-gray-300 p-1 mt-2 text-xl rounded-sm"
        ></list-item>
      </div>
    </div>
    <div v-else>
      Tidak tugas saat ini
    </div>

  </div>
</template>


<script>
import listItem from "./listItem";

export default {
  props: ["items"],
  components: { listItem },
};
</script>