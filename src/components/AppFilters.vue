<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        class="button"
        @click="setFilter('All')"
        :class="{ 'button--primary': activeFilter === 'All' }"
      >
        All
      </button>

      <button
        class="button"
        @click="setFilter('Active')"
        :class="{ 'button--primary': activeFilter === 'Active' }"
      >
        Active
      </button>

      <button
        class="button"
        @click="setFilter('Done')"
        :class="{ 'button--primary': activeFilter === 'Done' }"
      >
        Done
      </button>
    </section>
  </aside>
</template>
<script lang="ts">
import { Filter } from "@/models/Filter";
import { PropType, defineComponent } from "vue";

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
      required: true,
    },
  },
  methods: {
    setFilter(value: Filter) {
      this.$emit("setFilter", value);
    },
  },
  emits: {
    setFilter: (value: Filter) => value,
  },
});
</script>
