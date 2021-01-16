<template>
	<div class="card card-w70">    
		<h3 v-if="componentList.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
		<div v-else >
			<component :text="item.text" :is="item.type" v-for="item in componentList" :key="item"></component>     
		</div>		
	</div>
	
</template>

<script>
import AppTitle from './AppTitle'
import AppSubTitle from './AppSubTitle'
import AppAvatar from './AppAvatar'
import AppText from './AppText'
	export default {
		props : ['componentList'],
		components : {AppTitle, AppSubTitle, AppAvatar, AppText}
	}
</script>