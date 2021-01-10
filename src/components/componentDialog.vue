<template>
  <el-dialog
    title="Shipping address"
    :visible.sync="dialog"
    :before-close="handleCloseDialog"
  >
    <el-form>
      <el-input placeholder="Name" type="text" v-model="formData.name">
      </el-input>
      <el-input placeholder="Address" type="text" v-model="formData.address">
      </el-input>
      <template class="dialog-footer">
        <el-button @click="handleCloseDialog">Cancel</el-button>
        <el-button type="primary" @click="onSave">Save</el-button>
      </template>
    </el-form>
  </el-dialog>
</template>
<script>
const formDefault = {
  id: undefined,
  name: "",
  address: "",
};
export default {
  props: {
    visible: Boolean,
    formData: {
      type: Object,
      required: false,
      default: () => ({ ...formDefault }),
    },
    mode: {
      type: String,
      required: false,
      default: () => "",
    },
  },
  data() {
    return {
      dialog: this.visible,
    };
  },
  watch: {
    visible(val) {
      this.dialog = val;
    },
  },
  methods: {
    onSave() {
      const _form = { ...this.formData };
      this.$emit("onSubmit", _form);
      this.form = { ...formDefault };
      this.handleCloseDialog();
    },
    handleCloseDialog() {
      this.$emit("closeDialog", false);
    },
  },
};
</script>