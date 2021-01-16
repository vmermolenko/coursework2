<template>
	<form class="card card-w30" @submit.prevent="addComponent">
		<div class="form-control">
			<label for="type">Тип блока</label>
			<select id="type" v-model="addType">
				<option value="app-title">Заголовок</option>
				<option value="app-sub-title">Подзаголовок</option>
				<option value="app-avatar">Аватар</option>
				<option value="app-text">Текст</option>
			</select>
		</div>

		<div class="form-control">
			<label for="value">Значение</label>
			<textarea v-model="addText" id="value" rows="3"></textarea>
		</div>

		<button class="btn primary" :disabled="showBtn">Добавить</button>
	</form>
</template>

<script>
	export default {

		emits : ['actionaddblock'],
		data(){
			return {
				addType : 'app-title',
      	addText : '',
			}
		},
		computed : {
      showBtn(){
				return this.addText.length < 4
			}
		},
		methods : {
			addComponent(){
				this.$emit('actionaddblock', {
						type : this.addType,
						text : this.addText
					}
				)
				this.addType = 'app-title'
				this.addText = ''
			}
  	},
	}
</script>
