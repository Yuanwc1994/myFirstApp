<template>
	<view class="container">
		<!-- 输入区域 -->
		<view class="input-row">
			<input
				class="input"
				v-model="newTodo"
				placeholder="请输入待办事项"
				confirm-type="done"
				@confirm="addTodo"
			/>
			<button class="add-btn" type="primary" size="mini" @click="addTodo">添加</button>
		</view>

		<!-- 统计 -->
		<view class="stats">
			<text>共 {{ todos.length }} 项，已完成 {{ doneCount }} 项</text>
			<text v-if="todos.length" class="clear-btn" @click="clearDone">清除已完成</text>
		</view>

		<!-- 列表 -->
		<view class="list">
			<view v-if="!todos.length" class="empty">
				<text>暂无待办，快去添加吧~</text>
			</view>
			<view
				v-for="(item, index) in todos"
				:key="item.id"
				class="todo-item"
			>
				<view class="check-box" :class="{ checked: item.done }" @click="toggleTodo(index)">
					<text v-if="item.done" class="check-mark">✓</text>
				</view>
				<text class="todo-text" :class="{ done: item.done }">{{ item.text }}</text>
				<text class="delete-btn" @click="removeTodo(index)">删除</text>
			</view>
		</view>
	</view>
</template>

<script>
let idCounter = Date.now()

export default {
	data() {
		return {
			newTodo: '',
			todos: []
		}
	},
	computed: {
		doneCount() {
			return this.todos.filter(t => t.done).length
		}
	},
	onLoad() {
		this.loadTodos()
	},
	methods: {
		addTodo() {
			const text = this.newTodo.trim()
			if (!text) {
				uni.showToast({ title: '请输入内容', icon: 'none' })
				return
			}
			this.todos.unshift({
				id: ++idCounter,
				text,
				done: false
			})
			this.newTodo = ''
			this.saveTodos()
		},
		toggleTodo(index) {
			this.todos[index].done = !this.todos[index].done
			this.saveTodos()
		},
		removeTodo(index) {
			this.todos.splice(index, 1)
			this.saveTodos()
		},
		clearDone() {
			this.todos = this.todos.filter(t => !t.done)
			this.saveTodos()
		},
		saveTodos() {
			uni.setStorageSync('todos', JSON.stringify(this.todos))
		},
		loadTodos() {
			const raw = uni.getStorageSync('todos')
			if (raw) {
				try {
					this.todos = JSON.parse(raw)
				} catch (e) {
					this.todos = []
				}
			}
		}
	}
}
</script>

<style scoped>
.container {
	padding: 30rpx;
	background-color: #f5f5f5;
	min-height: 100vh;
	box-sizing: border-box;
}

.input-row {
	display: flex;
	align-items: center;
	gap: 20rpx;
	margin-bottom: 30rpx;
}

.input {
	flex: 1;
	height: 72rpx;
	padding: 0 24rpx;
	background-color: #ffffff;
	border-radius: 12rpx;
	font-size: 28rpx;
}

.add-btn {
	margin-left: 20rpx;
}

.stats {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 20rpx;
	font-size: 24rpx;
	color: #999;
}

.clear-btn {
	color: #007aff;
}

.list {
	background-color: #ffffff;
	border-radius: 12rpx;
	overflow: hidden;
}

.empty {
	padding: 80rpx 0;
	text-align: center;
	color: #bbb;
	font-size: 28rpx;
}

.todo-item {
	display: flex;
	align-items: center;
	padding: 24rpx 30rpx;
	border-bottom: 1rpx solid #f0f0f0;
}

.todo-item:last-child {
	border-bottom: none;
}

.check-box {
	width: 40rpx;
	height: 40rpx;
	border: 2rpx solid #ccc;
	border-radius: 50%;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-shrink: 0;
}

.check-box.checked {
	background-color: #007aff;
	border-color: #007aff;
}

.check-mark {
	color: #ffffff;
	font-size: 24rpx;
}

.todo-text {
	flex: 1;
	margin-left: 24rpx;
	font-size: 28rpx;
	color: #333;
	word-break: break-all;
}

.todo-text.done {
	color: #bbb;
	text-decoration: line-through;
}

.delete-btn {
	color: #ff4d4f;
	font-size: 24rpx;
	flex-shrink: 0;
	margin-left: 20rpx;
}
</style>
