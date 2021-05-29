<template>
	<div class="events">
		<h4>Accidents</h4>
		<ul class="events__list">
			<li
				class="card"
				:class="event.id === isActive ? 'active' : ''"
				v-for="event in events"
				:key="event.id"
				@click="selectEvent(event)"
			>
				<span class="card__title">{{ event.title }}</span>
			</li>
		</ul>
	</div>
</template>

<script>
//import { events } from '../assets/data.js';

export default {
	data() {
		return {
			//events: events,
			id: null,
			isActive: null
		};
	},
	props: ['events'],
	methods: {
		selectEvent(event) {
			this.isActive = event.id;
			this.$emit('selected', event);
		}
	}
};
</script>

<style lang="scss" scoped>
h4 {
	margin-bottom: 10px;
}

.events {
	border: 1px solid black;
	border-radius: 5px;
	padding: 15px;
	background-color: #e5e5e5;
	height: 100%;
	&__list {
		padding-left: 0px !important;
		list-style-type: none;
	}
}

.card {
	border: 1px solid black;
	border-radius: 5px;
	padding: 15px;
	margin-bottom: 10px;
	background: white;
	box-shadow: 2px 3px 7px 0px #5f5f5f;
}

.active {
	border: 2px solid #9bd5c5;
}
</style>
