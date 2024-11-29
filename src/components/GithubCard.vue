<script setup>
	import { ref } from 'vue';

	const props = defineProps({
		username: { type: String, required: true },
	});

	const user = ref();

	fetch(`https://api.github.com/users/${props.username}`).then(
		async (response) => {
			const data = await response.json();
			user.value = data;
		}
	);
</script>
<template>
	<div
		v-if="user"
		class="card card-side bg-base-100 shadow-xl m-5"
	>
		<figure>
			<img
				:src="user.avatar_url"
				alt="Movie"
			/>
		</figure>
		<div class="card-body">
			<h2 class="card-title">{{ user.name }}</h2>
			<p>
				{{ user.bio }}
			</p>
			<div class="card-actions justify-end">
				<a
					:href="user.html_url"
					class="btn btn-primary"
					>View Profile</a
				>
			</div>
		</div>
	</div>
</template>
