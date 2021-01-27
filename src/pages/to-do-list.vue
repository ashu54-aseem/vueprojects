<template>
  <div class="m-auto">
    <h1 class="text-3xl text-center my-4">To-Do-List {{ itemsCount }}</h1>
    <ul class="border rounded p-2">
      <li
        class="flex justify-between"
        v-for="(item, index) in to-do-list"
        :key="item.name"
      >
        <div>
          {{ item.name }}
        </div>
        <button v-on:click="remove(index)">x</button>
      </li>
    </ul>
    <form class="mt-10" @submit.prevent="addTtem">
      <input
        class="border rounded px-2"
        v-model="newItem"
        placeholder="Type Item Name Here"
        ref="newHeroRef"
      />
      <button
        class="border rounded bg-gradient-to-r from-red-700 to-pink-500 text-white ml-2 px-2"
        type="submit"
      >
        Add Item
      </button>
    </form>
  </div>
</template>

<script>
import { computed, onMounted, ref } from "vue";
export default {
  setup() {
    const newItemRef = ref("");
    const newItem = ref("");
    const to-do-list = ref([
      { name: "Breakfast" },
      { name: "Excersise" },
      { name: "Lunch" },
      { name: "Study" },
      { name: "Dinner" },
    ]);

    onMounted(() => {
      newItemRef.value.focus();
    });

    const itemsCount = computed({
      get: () => to-do-list.value.length,
    });

    function remove(index) {
      to-do-list.value = to-do-list.value.filter((item, i) => i != index);
    }

    function addItem() {
      if (newItem.value !== "") {
        to-do-list.value.unshift({ name: newItem.value });
        newItem.value = "";
      }
    }

    return { to-do-list, newItem, remove, addItem, newItemRef, itmesCount };
  },
};
</script>

<style></style>
