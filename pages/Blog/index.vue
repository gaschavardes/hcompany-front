<template>
	<div>
	  <h1>Blogs</h1>
	  {{ response }}
	</div>
  </template>

<script lang="ts" setup>
	import type { Blog } from '~/types'
	const route = useRoute()
	const { findOne } = useStrapi()

	// const { data: articles, pending, error, refresh} = await useAsyncData
	// ("blog", () => findOne("blogs", route.params.id), {
	// 	default: () => ({ data: []})
	// })

	const response = await findOne<Blogs>('blogs');

	const click =  () => {
		console.log('CLICK')
	}

	onMounted(() => {
		console.log(route.params.id)
	})

</script>

