<template>
  <div class="component-editor">
    <el-form>
      <h5>Component props</h5>
      <el-form-item
        v-for="(prop, key) in componentProps"
        :label="key"
        :key="key"
      >
        <component :is="mappings[prop.type]" v-model="config[key]"> </component>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  name: "component-editor",
  props: {
    componentProps: {
      type: Object,
      default: () => ({})
    }
  },
  data() {
    return {
      mappings: {
        String: "el-input",
        Boolean: "el-switch",
        default: "el-input"
      },
      config: {}
    };
  },
  watch: {
    config: {
      deep: true,
      handler(newValue) {
        this.$emit("change", newValue);
      }
    }
  }
};
</script>
<style lang="scss">
.component-editor {
  padding: 10px;
  .el-form .el-form-item {
    margin-bottom: 0;
  }
  .el-form .el-form-item__label {
    line-height: 25px;
  }
}
</style>
