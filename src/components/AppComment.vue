<template>
	<p>
		<button class="btn primary" @click="loadComments">Загрузить комментарии</button>
	</p>
	<div class="card" v-if="comments.length > 0">
		<h2>Комментарии</h2>
		<ul class="list">
			<li class="list-item" v-for="item in comments" :key="item.id">
				<div>
					<p><strong>{{ item.email }}</strong></p>
					<small>{{ item.body }}</small>
				</div>
			</li>
		</ul>
	</div>
	<app-loader v-if="loading"></app-loader>
</template>

<script>
import AppLoader from './AppLoader'
import axios from 'axios'
	export default {
		data(){
			return {
				comments : [],
				loading : false
			}
		},
		methods : {
			async loadComments(){
				this.comments = []
				this.loading = true
				try {
					const url = 'https://jsonplaceholder.typicode.com/comments?_limit=42'
				
					const {data} = await axios.get(url)
					if (!data) {
						throw new Error('Список комметариев пуст') 
					}

					this.comments = Object.keys(data).map( key => {
						return {
							id: key,
							...data[key]
						}
					})
					this.loading = false
				} catch (e) {
					this.loading = false
				}
			}
		},
		components : { AppLoader }
	}
</script>
