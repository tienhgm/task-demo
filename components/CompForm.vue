<template>
  <el-form prop="noti" ref="ruleForm" label-width="100px">
    <el-form-item prop="name" label="Name" class="form-item">
      <el-input
        v-model="ruleForm.name"
        placeholder="name"
        autocomplete="off"
        class="input-form"
      />
      <div class="error">
        {{ !$v.ruleForm.name.required ? "Field is required" : "" }}
      </div>
    </el-form-item>
    <el-form-item prop="content" label="Content" class="form-item">
      <el-input
        v-model="ruleForm.content"
        type="textarea"
        placeholder="content"
        autocomplete="off"
        class="input-form"
      />
      <div class="error">
        {{ !$v.ruleForm.content.required ? "Field is required" : "" }}
      </div>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click.prevent="alertForm()">Submit</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
import { required } from "vuelidate/lib/validators";
export default {
    name: 'comp-form',
    data(){
        return {
            ruleForm: {
                name: "",
                content: "",
            },
        }
    },
    validations: {
        ruleForm: {
            name: {
                required
            },
            content: {
                required
            },
        },
	},
    methods:{
        alertForm() {
            const invalid = this.$v.ruleForm.$invalid;
            if (invalid) {
                this.$v.ruleForm.$touch();
                this.$notify.error({
                    title: "Error",
                    duration: 2000,
                });
                return;
            }
            this.$notify.success({
                title: "Notification",
                message: `Name: ${this.ruleForm.name}, Content: ${this.ruleForm.content}`,
                duration: 2000,
            });
            let objForm = {
                name: this.ruleForm.name,
                content: this.ruleForm.content,
            };
            this.$emit('handleAddForm',objForm)
            this.handleResetForm();
        },
        handleResetForm() {
            this.ruleForm.name = "";
            this.ruleForm.content = "";
        },
    }
   
};
</script>

<style scoped>
.error {
	display: block;
	font-weight: 400;
	line-height: 20px;
	color: #eb5757;
	font-size: 12px;
}
</style>