<template>
  <el-dialog
    title="Shipping address"
    :visible.sync="dialog"
    :before-close="handleCloseDialog"
  >
    <el-form>
      <el-input placeholder="Name" type="text" v-model="form.name"> </el-input>
      <el-input placeholder="Address" type="text" v-model="form.address">
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
      form: { ...this.formData },
    };
  },
  watch: {
    visible(val) {
      this.dialog = val;
    },
  },
  methods: {
    onSave() {
      //   console.log(this.form);
      const _form = { ...this.form };
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