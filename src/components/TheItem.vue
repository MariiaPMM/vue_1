<template>
	<li
		v-for="todo in todoList"
		:key="todo.id"
		class="list__item"
	>
		<div>
			<input
				v-model="todo.completed"
				:checked="todo.completed"
				type="checkbox"
			/>
			<span
				v-if="editingTodoId !== todo.id"
				:class="{
					completed: todo.completed,
					uncompleted: !todo.completed,
				}"
				@dblclick="editingTodoId = todo.id"
			>
				{{ todo.title }}
			</span>
			<input
				v-else
				v-model="todo.title"
				type="text"
				@blur="editingTodoId = null"
			/>
		</div>
		<button
			class="btn_delete"
			@click="deleteTodo(todo)"
		>
			X
		</button>
	</li>
</template>
<script>
export default {
	name: 'TheList',
	props: {
		todo: {
			type: Object,
			default: () => {},
		},
	},
	data() {
		return {
			isEditing: false,
		};
	},
};
</script>
<style scoped lang="scss">
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
