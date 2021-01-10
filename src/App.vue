<template>
  <div>
    <el-card class="box-card" slot="header">
      <el-button type="text" size="small" @click="onAdd">Add</el-button>
    </el-card>
    <el-table style="width: 100%" :data="data">
      <el-table-column prop="name" label="Name" width="500"> </el-table-column>
      <el-table-column prop="address" label="Address" min-width="180">
      </el-table-column>
      <el-table-column label="Action">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="onEdit(scope.row)"
            >Edit</el-button
          >
          <el-button
            type="text"
            size="small"
            @click.native.prevent="onRemove(scope.$index, data)"
            >Remove</el-button
          >
        </template>
      </el-table-column>
    </el-table>
    <component-dialog
      :visible.sync="dialog"
      :formData="form"
      :mode="mode"
      @closeDialog="onCloseDialog"
      @onSubmit="handleSubmit"
    />
  </div>
</template>

<script>
import ComponentDialog from "./components/componentDialog.vue";
const defaultForm = {
  id: undefined,
  name: "",
  address: "",
};
export default {
  name: "App",
  components: {
    ComponentDialog,
  },

  data() {
    return {
      dialog: false,
      form: { ...defaultForm },
      mode: "ADD",
      data: [
        {
          id: 1,
          name: "Note 1",
          address: "adsadsd",
        },
      ],
    };
  },

  methods: {
    handleSubmit(_form) {
      if (this.mode === "ADD") {
        this.data.push({
          id: Math.round(Math.random() * 10000),
          name: _form.name,
          address: _form.address,
        });
      } else {
        const _form = { ...this.form };
        const index = this.data.findIndex((item) => item.id === _form.id);
        this.data.splice(index, 1, { ..._form });
        this.mode = "ADD";
      }
      this.form = { ...defaultForm };
    },
    onAdd() {
      this.mode = "ADD";
      this.dialog = true;
    },
    onEdit(dataEdit) {
      this.mode = "EDIT";
      const _dataEdit = { ...dataEdit };
      this.form = { ..._dataEdit };
      this.dialog = true;
    },
    onRemove(index, rows) {
      rows.splice(index, 1);
    },
    onCloseDialog(val) {
      // console.log(val);
      this.dialog = val;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
