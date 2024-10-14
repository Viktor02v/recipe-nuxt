<script setup lang="ts">

</script>

<template>
	<header class="py-4 w-full border-b">
		<nav class="flex container  items-center">
			<NuxtLink to="/" class="flex gap-1 items-center">
				<img class="w-8 md:w-14 lg:w-14" src="/icon-green.png" alt="" />
				<span class=" sm:text-2xl md:text-3xl lg:text-3xl font-bold">Nuxtcipes</span>
			</NuxtLink>
			<ul
				class="flex text-sm gap-6 ml-auto md:text-xl lg:text-xl font-extrabold md:font-bold lg:font-bold capitalize">
				<li>
					<NuxtLink to="/">Home</NuxtLink>
				</li>
				<li>
					<NuxtLink to="/about">About</NuxtLink>
				</li>
			</ul>
		</nav>
	</header>
</template>
