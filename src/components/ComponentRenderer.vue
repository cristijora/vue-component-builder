<template>
  <component
    class="draggable-component"
    :key="index"
    :is="componentData.component"
    @click.native.stop="componentClick(componentData.component, index);"
    v-bind="componentData.props"
  >
    <draggable
      v-for="slotName in componentData.slots"
      :key="slotName"
      class="slot-box"
      :options="dragOptions"
      v-model="componentData.children"
      :slot="slotName"
    >
      <component-renderer
        v-for="(child, index) in componentData.children"
        :drag-options="dragOptions"
        :component-data="child"
        :index="index"
        @component-click="componentClick"
        :key="index"
      >
      </component-renderer>
      <div v-if="componentData.children.length === 0">{{ slotName }}</div>
    </draggable>
  </component>
</template>
<script>
import Draggable from "vuedraggable";
export default {
  name: "component-renderer",
  components: {
    Draggable
  },
  props: {
    componentData: {
      type: Object,
      default: () => ({})
    },
    dragOptions: {
      type: Object,
      default: () => ({})
    },
    index: {
      type: Number,
      default: 0
    }
  },
  methods: {
    componentClick(component, index) {
      this.$emit("component-click", component, index);
    }
  }
};
</script>
<style>
.slot-box {
  border: 1px dashed #ebeef5;
  min-height: 35px;
}
</style>
