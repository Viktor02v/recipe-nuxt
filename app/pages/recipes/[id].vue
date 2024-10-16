<script setup lang="ts">
import { type Recipe } from '../../../types/types';
const { id } = useRoute().params

const { data, error } = await useFetch<Recipe>(`https://dummyjson.com/recipes/${id}`)

if (error.value) {
	throw createError({
		statusCode: error.value?.statusCode,
		statusMessage: error.value?.statusMessage,
	})
}

useSeoMeta({
	title: data.value?.name,
	description: "Recepies by Recipe App",
	ogTitle: data.value?.name,
	ogDescription: "Recepies by Recipe App",
	ogImage: data.value?.image,
	ogUrl: `https://localhost:3000/recipes/${data.value?.id}`,
	twitterTitle: data.value?.name,
	twitterDescription:"Recepies by Recipe App",
	twitterImage:  data.value?.image,
	twitterCard: 'summary'
})
</script>

<template>
	<div class="flex flex-col h-[100vh] max-w-screen-lg container mb-20 py-20">
		<!-- Header -->
		<div class="flex flex-col mb-6">
			<h2 class="text-5xl mb-4 font-semibold">{{ data?.name }}</h2>
			<div class="flex gap-4 text-xl mb-6">
				<div class="flex items-center gap-1">
					<Icon name="mdi:clock-time-eight-outline" style="color: #f79f1a" />
					<span>{{ data?.cookTimeMinutes }}</span>
				</div>
				<div class="flex items-center gap-1">
					<Icon name="mdi:fire" style="color: #f79f1a" />
					<span>{{ data?.caloriesPerServing }}</span>
				</div>
				<div class="flex items-center gap-1">
					<Icon name="mdi:star" style="color: #f79f1a" />
					<span>{{ data?.rating }} ({{ data?.reviewCount }})</span>
				</div>
			</div>
			<hr />
		</div>

		<!-- Image -->
		<NuxtImg :src="data?.image" densities="x1" sizes="xs:100vw sm:100vw md:100vw lg:100vw"
			class="w-full max-h-[500px] object-cover rounded-md shadow-sm mb-12" alt="" />

		<!-- Ingredients -->
		<div class="mb-8">
			<h2 class="text-3xl font-semibold mb-4">Ingredients</h2>
			<ul class="grid grid-cols-1 md:grid-cols-2 gap-2 text-lg">
				<li v-for="ingredient in data?.ingredients" :key="ingredient">
					<label class="flex gap-2 items-center">
						<input class="hidden peer" type="checkbox" />
						<div
							class="relative w-6 h-6 rounded-full border-2 border-dodgeroll-gold flex items-center justify-center peer-checked:after:absolute peer-checked:after:w-4 peer-checked:after:h-4 peer-checked:after:bg-dodgeroll-gold peer-checked:after:rounded-full">
						</div>
						<span class="peer-checked:line-through">
							{{ ingredient }}
						</span>
					</label>
				</li>
			</ul>
		</div>

		<!-- Instructions -->
		<div>
			<h2 class="text-3xl font-medium mb-4">Instructions</h2>
			<ul>
				<li v-for="(instruction, index) in data?.instructions" :key="instruction" class="flex flex-col gap-2">
					<span class="flex items-center justify-center w-5 h-5 p-2 bg-dodgeroll-gold text-white text-sm">
						{{ index + 1 }}
					</span>
					<span class="flex-1">{{ instruction }}</span>
				</li>
			</ul>
		</div>
	</div>
</template>

<style scoped></style>
