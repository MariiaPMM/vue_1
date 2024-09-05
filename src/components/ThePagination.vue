<template>
	<div class="pagination">
		<button
			v-for="page in pagesCount"
			:key="page"
			:class="{ active: page === this.page }"
			@click="currentPage = page"
		>
			{{ page }}
		</button>
	</div>
</template>
<script>
export default {
	name: 'ThePaginatioon',
	emits: ['update:page'],
	props: {
		pagesCount: {
			type: Number,
			default: 1,
		},
		page: {
			type: Number,
			default: 1,
		},
	},
	computed: {
		currentPage: {
			get() {
				return this.page;
			},
			set(value) {
				this.$emit('update:page', value);
			},
		},
	},
};
</script>
<!-- <style scoped lang="sccs"> -->


.pagination {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 10px;
	margin-top: 10px;
	button {
		width: 30px;
		height: 30px;
		margin: 0;
		border-radius: 5px;
		border: 1px solid rgb(255, 255, 255);
		cursor: pointer;
		&.active {
			background: rgb(255, 255, 255);
			border: 1px solid rgb(255, 255, 255);
			pointer-events: none;
			color: black;
			width: 32px;
			height: 32px;
			font-size: 14px;
			box-shadow: 0px 0px 8px rgba(255, 255, 255, 0.5);
		}
		&:hover {
			border: 2px solid rgb(255, 255, 255);
			box-shadow: 0px 0px 8px rgba(255, 255, 255, 0.5);
		}
	}
}
<!-- </style> -->
