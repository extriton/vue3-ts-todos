<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        class="button"
        :class="{ 'button--primary': filter === activeFilter }"
        @click="setFilter(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { TFilter } from "@/types/TFilter";

interface State {
  filters: TFilter[];
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<TFilter>,
      required: true,
    },
  },
  data(): State {
    return {
      filters: ["All", "Active", "Done"],
    };
  },
  methods: {
    setFilter(filter: TFilter) {
      this.$emit('setFilter', filter)
    }
  },
  emits: {
    setFilter: (filter: TFilter) => filter
  }
});
</script>
