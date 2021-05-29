<template>
	<div class="accident">
		<h2 class="accident__title">{{ event.title }}</h2>
		<h5>Crée le {{ this.eventDate }} à {{ this.eventTime }} par {{ event.createdBy }}</h5>
		<div class="form-group">
			<label for="title">Titre</label>
			<input class="form-control" type="text" name="title" id="title" v-model="event.title" />
		</div>

		<div class="">
			<label for="description">Description</label>
			<textarea
				class="form-control"
				name="description"
				id="description"
				cols="30"
				rows="5"
				v-model="event.description"
			></textarea>
		</div>

		<div class="row">
			<div class="col-6 form-group">
				<label for="date">Date</label>
				<input class="form-control" type="date" name="date" id="date" v-model="eventDate" />
			</div>
			<div class="col-6 form-group">
				<label for="time">Heure</label>
				<input class="form-control" type="time" name="time" id="time" v-model="eventTime" />
			</div>
		</div>

		<div class="form-group">
			<label for="status">Statut</label>
			<select class="form-control" name="status" id="status" v-model="event.statusName">
				<option value="Open">Ouvert</option>
				<option value="InProgress">En Cours</option>
				<option value="Closed">Fermé</option>
			</select>
		</div>

		<div class="form-group">
			<label for="employee">Employé impliqué</label>
			<select v-model="event.involvedEmployeeId" class="form-control" type="text" name="employee" id="employee">
				<option v-for="employee in employees" :key="employee.id" :value="employee.id">
					{{ employee.firstname }} {{ employee.lastname }} ({{ employee.id }})
				</option>
			</select>
		</div>
		<div class="form-group">
			<label for="">Témoins</label>
			<div class="witness__container">
				<div class="witness" v-for="witness in event.witness" :key="witness">
					<span type="text" class="witness__input">{{ witness }}</span>
					<span class="witness__delete" @click="deleteWitness(witness)">X</span>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import { employees } from '../assets/data.js';
import moment from 'moment';
export default {
	props: ['event'],
	data() {
		return {
			eventDate: null,
			eventTime: null,
			employees: employees
		};
	},
	created() {
		// Format date on creation of the component
		this.formatDate();
	},
	updated() {
		// Format the date each time we change the event.
		this.formatDate();
	},
	methods: {
		formatDate() {
			this.eventTime = moment(String(this.event.creationDate)).format('HH:mm');
			this.eventDate = moment(String(this.event.creationDate)).format('YYYY-MM-DD');
		},
		deleteWitness(comment) {
			this.$emit('witnessDelete', comment);
		}
	}
};
</script>

<style lang="scss" scoped>
.accident {
	display: flex;
	flex-direction: column;
	text-align: left;
	margin: 0px 30px;
	color: #707070;
}

.witness {
	background-color: #9bd5c5;
	border-radius: 5px;
	margin-right: 5px;
	padding: 3px 10px;

	&__container {
		background-color: #fff;
		border-radius: 5px;
		border: 1px solid black;
		padding: 10px;
		display: flex;
		flex-wrap: wrap;
		justify-content: flex-start;
	}

	&__input {
		margin-right: 10px;
	}

	&__delete {
		font-weight: bold;
		cursor: pointer;
	}
}

label {
	color: #707070;
	font-weight: 600;
	font-size: 14px;
}

.date {
	display: flex;
	justify-content: space-between;
}
</style>
