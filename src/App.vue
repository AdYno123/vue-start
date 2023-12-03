<script>
export default {
  data() {
    return {
      input: "",
      list: [],
    };
  },
  methods: {
    /**
     * add item to list
     */
    addItem() {
      if (this.input === "") {
        return;
      }
      this.list.push({
        id: this.list.length + 1,
        text: this.input,
        is_deleted: false,
      });
      this.input = "";
    },
    /**
     * remove item from list
     */
    deleteItem(item) {
      item.is_deleted = true;
    },
  },
  computed: {
    /**
     * Return only valid items in list
     */
    validItems() {
      return this.list.filter((item) => !item.is_deleted);
    },

    /**
     * Return only is_deleted items in list
     */
    deletedItems() {
      return this.list.filter((item) => item.is_deleted);
    },
  },
};
</script>

<template>
  <div class="container mx-auto bg-white p-5">
    <section>
      <input
        v-model="input"
        class="w-1/2 border-2 border-black"
        placeholder="Add Item Here..."
      />
      <button
        @click="addItem()"
        class="bg-green-500 rounded-lg mx-3 p-2 text-white font-bold"
      >
        Add to list
      </button>
    </section>

    <section class="mt-5">
      <h1 class="text-3xl font-bold">Položky:</h1>
      <ul>
        <li v-for="item in validItems" :key="`item-${item.id}`">
          <span @click="deleteItem(item)" class="mt-4">X</span>
          {{ item.text }}
        </li>
      </ul>
    </section>
    <section>
      <h2 class="text-3xl font-bold">Vymazané Položky:</h2>
      <ul>
        <li
          v-for="item in deletedItems"
          :key="`item-${item.id}`"
          class="line-through"
        >
          <span @click="deleteItem(item)" class="mt-4">X</span>
          {{ item.text }}
        </li>
      </ul>
    </section>
  </div>
</template>
