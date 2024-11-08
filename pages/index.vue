<template>
	<div>
	  
	  {{ response }}
	  <div class="blog-list">
		<router-link v-for="blog in blogs.data" :key="blog.documentId">{{ blog.title }}</router-link>
	  </div>
	</div>
  </template>

<script lang="ts" setup>
	// import type { Blog } from '~/types'
	const route = useRoute()
	const { findOne, find } = useStrapi()

	// const { data: articles, pending, error, refresh} = await useAsyncData
	// ("blog", () => findOne("blogs", route.params.id), {
	// 	default: () => ({ data: []})
	// })

	const response = await findOne<Home>('home', '?populate=*');
	const blogs = await findOne<Blogs>('blogs');

	const click =  () => {
		console.log('CLICK')
	}

	onMounted(() => {
		console.log(route.params.id)
	})

</script>

