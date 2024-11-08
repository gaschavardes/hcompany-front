<template>
	<div>
		<h1>Blog Single</h1>
		{{ response.data[0] }}

		<div class="content">
			<div v-for="(item, id) in response.data[0].content" :key="id">
				{{ item.__component.replace('common.', '').charAt(0).toUpperCase() + item.__component.replace('common.', '').slice(1) }}
				<component v-if=" item.__component.replace('common.', '') === 'title1'" :is="title1" />
				<component v-else-if=" item.__component.replace('common.', '') === 'title2'" :is="title2" />
				<component v-else-if=" item.__component.replace('common.', '') === 'title3'" :is="title3" />
				<component v-else-if=" item.__component.replace('common.', '') === 'title4'" :is="title4" />
				<component v-else-if=" item.__component.replace('common.', '') === 'text'" :is="text" />
				<component v-else:is="image" />
			</div>
		</div>
	</div>
</template>

<script lang="ts" setup>
import type { Blog } from '~/types'
import { Title1 } from '#components'
const route = useRoute()
const { findOne } = useStrapi()

const title1 = resolveComponent('Title1')
const title2 = resolveComponent('Title2')
const title3 = resolveComponent('Title3')
const title4 = resolveComponent('Title4')
const text = resolveComponent('Text')
const image = resolveComponent('Image')

// const { data: articles, pending, error, refresh} = await useAsyncData
// ("blog", () => findOne("blogs", route.params.id), {
// 	default: () => ({ data: []})
// })

const response = await findOne<Blogs>('blogs', `?filters\[slug\][$eq]=${route.params.id}&populate=*`);

const click = () => {
	console.log('CLICK')
}

onMounted(() => {
	console.log(route.params.id)
})

</script>
