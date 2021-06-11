<template>
	<div class="container">
        <div class="left-content">
            <comp-form v-on:handleAddForm="handleAddForm" />
        </div>
        <div class="right-content">
            <list-message :listInfo="listInfo"/>
        </div>
	</div>
</template>

<script>

export default {
	name: "notification",
	data() {
        return {
            listInfo: []
        };
	},
	methods: {
        handleAddForm(objForm){
            this.listInfo.push(objForm)
        }
	}
};
</script>

<style>
.container {
	margin-top: 300px;
}
.left-content {
	float: left;
	width: 35%;
}
.right-content {
	float: right;
	width: 50%;
}
</style>