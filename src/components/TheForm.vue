<template>
	<form @submit.prevent="addTodo">
		<div>
			<input
				v-model="newTodo"
				type="text"
			/>
			<button class="btnAdd">Add</button>
		</div>
		<div>
			<span>Filter by:</span>
			<select v-model="selectedFilter">
				<option value="all">All</option>
				<option value="completed">Completed</option>
				<option value="uncompleted">Uncompleted</option>
			</select>
		</div>
		<div>
			<span>limit:</span>
			<select v-model="selectedLimit">
				<option value="10">10</option>
				<option value="15">15</option>
				<option value="20">20</option>
			</select>
		</div>
	</form>
</template>
<script>
export default {
	name: 'TheForm',
	emits: ['add-todo', 'update:filter', 'update:limit'],
	data() {
		return {
			newTodo: '',
		};
	},
  props: {
		filter: {
			type: String,
			default: 'all',
		},
		limit: {
			type: Number,
			default: 10,
		},
	},
  computed: {
		selectedFilter: {
			get() {
				return this.filter;
			},
			set(value) {
				this.$emit('update:filter', value);
			},
		},
		selectedLimit: {
			get() {
				return this.limit;
			},
			set(value) {
				this.$emit('update:limit', value);
			},
		},
	},
	methods: {
		addTodo() {
			this.$emit('add-todo', this.newTodo);
			this.newTodo = '';
		},
	},
};
</script>

<!-- <style scoped lang="scss"> -->
button {
	margin: 0 10px;
	background-color: rgba(39, 39, 45, 0.385);
	border-radius: 50%;
	border: 1px solid #fff;
	color: #fff;
	width: 25px;
	height: 25px;
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
<!-- </style> -->
