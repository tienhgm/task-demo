<template>
	<div class="container">
        <div class="left">
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
                    <el-button type="primary" @click.prevent="alertForm()"
                    >Submit</el-button
                    >
                </el-form-item>
            </el-form>
        </div>
        <div class="right">
            <table class="list-table">
                <thead>
                    <tr>
                        <th>#</th>
                        <th style="width:300px">List</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(e, index) in listInfo" :key="index">
                        <td>{{++index}}</td>
                        <td>
                            <div class="name">
                                {{ e.name }}
                            </div>
                            <div class="content">
                                {{ e.content }}
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
	</div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
export default {
	name: "notification",
	data() {
        return {
            ruleForm: {
                name: "",
                content: "",
            },
            listInfo: [],
        };
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
	methods: {
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
            this.listInfo.push(objForm);
            this.handleResetForm();
        },
        handleResetForm() {
            this.ruleForm.name = "";
            this.ruleForm.content = "";
        },
	}
};
</script>

<style>
.container {
	margin-top: 300px;
}
.left {
	float: left;
	width: 35%;
}
.right {
	float: right;
	width: 50%;
}
.error {
	display: block;
	font-weight: 400;
	line-height: 20px;
	color: #eb5757;
	font-size: 12px;
}
table tr {
	border-top: 1px solid #ccc;
	border-bottom: 1px solid #ccc;
}
table {
	border-collapse: collapse;
}
th, td {
	text-align: left;
	width: 120px;
}
table .name{
    font-size:12px;
    color: #D798C1;
    font-weight: bold;
    line-height: 20px;
}
</style>