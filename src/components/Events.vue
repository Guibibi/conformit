<template>
	<div>
		<div class="card" v-for="event in events" :key="event.id">
			<p>{{ event.title }}</p>
		</div>
	</div>
</template>

<script>
import { events } from '../assets/data.js';

export default {
	data() {
		return {
			events: events
		};
	},
	mounted() {
		console.log(this.events);
	}
};
</script>

<style lang="scss" scoped></style>
