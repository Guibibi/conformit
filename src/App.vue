<template>
	<div id="app">
		<div class="container-fluid row">
			<div class="events col-md-4">
				<Events-list :events="eventsList" @selected="selectedEvent"></Events-list>
			</div>
			<div class="accident col-md-4">
				<Accident :event="event"></Accident>
			</div>
			<div class="comments col-md-4">
				<Comment :comments="comments"></Comment>
			</div>
		</div>
	</div>
</template>

<script>
import EventsList from './components/EventList.vue';
import Accident from './components/Accident';
import Comment from './components/Comments';
import { events, GetEventComments } from './assets/data';

export default {
	name: 'App',
	components: {
		EventsList,
		Accident,
		Comment
	},
	data() {
		return {
			eventsList: events,
			event: null,
			comments: []
		};
	},
	methods: {
		selectedEvent(event) {
			this.event = event;
			this.comments = GetEventComments(event.id);
		}
	},
	created() {
		// Select the first event by default
		this.selectedEvent(this.eventsList[0]);
	}
};
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
	width: 100vw;
	height: 100vh;
}
</style>
