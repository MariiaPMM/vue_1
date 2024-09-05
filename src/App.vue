<template>
	<div class="row">
		<span>Total: {{ todosCount }}</span>

		<TheForm
			@add-todo="addTodo"
			v-model:filter="filter"
			v-model:limit="limit"
		/>
		<TheList
			@delete-todo="deleteTodo"
			v-if="todoList?.length"
			:list="todoList"
		/>
		<ThePagination
			v-if="todosCount"
			v-model:page="page"
			:pages-count="pagesCount"
		/>
	</div>
</template>

<script>
import axios from 'axios';
import TheForm from './components/TheForm.vue';
import TheList from './/components/TheList.vue';
import ThePagination from './components/ThePagination.vue';
export default {
	components: {
		TheForm,
		TheList,
		ThePagination,
	},
	data() {
		return {
			baseUrl: 'https://jsonplaceholder.typicode.com/',
			todoList: [],
			newTOdo: '',
			filter: 'all',
			editingTodoId: null,
			limit: 10,
			page: 1,
			todosCount: null,
		};
	},
	async created() {
		await this.getTodos();
		await this.getTodos({
			_limit: this.limit,
			_page: this.page,
		});
	},
	computed: {
		isFiltered() {
			return this.filter !== 'all';
		},
		pagesCount() {
			return Math.ceil(this.todosCount / this.limit);
		},
	},
	watch: {
		async limit() {
			await this.getTodosBy();
		},
		async page() {
			await this.getTodosBy();
		},
		async filter() {
			this.page = 1;

			if (this.isFiltered) {
				await this.getTodos({
					completed: this.filter === 'completed',
				});

				await this.getTodos({
					_limit: this.limit,
					_page: this.page,
					completed: this.filter === 'completed',
				});
			}

			if (this.filter === 'all') {
				await this.getTodos();

				await this.getTodos({
					_limit: this.limit,
					_page: this.page,
				});
			}
		},
	},
	methods: {
		async getTodosBy() {
			const params = {
				_limit: this.limit,
				_page: this.page,
			};

			if (this.isFiltered) {
				params.completed = this.filter === 'completed';
			}
			await this.getTodos(params);
		},
		async getTodos(params = null) {
			try {
				const { data } = await axios.get(`${this.baseUrl}todos`, { params });

				if (!params || !params?._limit) {
					this.todosCount = data.length;
				} else this.todoList = data;
			} catch (error) {
				console.log('getTodos ~ error:', error);
			}
		},
		async deleteTodo(todoId) {
			this.todoList = this.todoList.filter(item => item.id !== todo.id);
		},
		addTodo(newTodo) {
			if (!todo) return;
			this.todoList.unshift({
				completed: false,
				id: Date.now(),
				title: todo,
			});
		},
	},
};
</script>

<style scoped lang="scss">
.row {
	font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	width: 100vw;
	min-height: 100vh;
	.row_container {
		display: flex;
		flex-direction: column;
		justify-content: start;
		margin: 0 0px 10px;
		color: #fff;
		span {
			margin: 0 0 10px;
		}
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
	.btnAdd {
		width: 90px;
		height: 25px;
		border-radius: 5px;
		color: #fff;
		&:hover {
			background-color: rgba(24, 24, 26, 0.21);
			box-shadow: 0px 0px 8px rgba(255, 255, 255, 0.5);
		}
		&:active {
			background-color: rgba(24, 24, 26, 0.751);
			border: 2px solid #fff;
		}
	}

	span,
	input[type='text'] {
		margin: 0 10px;
		font-weight: 500;
		font-family: URW Chancery L, cursive;
		border-radius: 5px;
		border: none;
		&:focus {
			box-shadow: 0px 0px 8px rgba(255, 255, 255, 0.5);
		}
	}
}
</style>
