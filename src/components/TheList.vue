<template>
	<ul class="list">
		<TheItem
			v-for="todo in list"
			:key="todo.id"
			:todo="todo"
			@delete-todo="$emit('delete-todo', $event)"
		/>
	</ul>
</template>
<script>
import TheItem from './TheItem.vue';
export default {
	components: { TheItem },
	name: 'TheList',
	props: {
		list: {
			type: Array,
			default: () => [],
		},
	},
};
</script>

<style scoped lang="scss">
ul {
	border-radius: 15px;
	width: 700px;
	list-style-type: none;
	display: flex;
	flex-direction: column;
	margin: 0;
	padding: 0;
	border: 1px solid rgb(255, 255, 255);
	box-shadow: 0px 0px 8px rgba(255, 255, 255, 0.5);
}
li {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 10px 5px;
	text-transform: capitalize;

	&:nth-child(odd) {
		border: solid 1px #fff;
		border-radius: 15px;
	}
}
.completed {
	color: rgb(255, 255, 255);
}
.uncompleted {
	color: rgb(155, 202, 252);
}
button {
	margin: 0 10px;
	background-color: rgba(39, 39, 45, 0.385);
	border-radius: 50%;
	border: 1px solid #fff;
	color: #fff;
	width: 25px;
	height: 25px;
}
.btn_delete {
	&:hover {
		background: rgba(102, 102, 131, 0.723);
		font-weight: 700;
		color: rgba(24, 24, 26);
		&:active {
			box-shadow: 0px 0px 8px rgba(255, 255, 255, 0.5);
		}
	}
}
</style>
