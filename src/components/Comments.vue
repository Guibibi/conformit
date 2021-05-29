<template lang="html">
	<div class="comment">
		<h4>Commentaires</h4>
		<div v-for="comment in comments" :key="comment" class="comment__card">
			<div class="d-flex">
				<b-icon-person-circle class="comment__picture" font-scale="2"></b-icon-person-circle>
				<div class="comment__info">
					<span class="comment__author">{{ comment.author }}</span>
					<br />
					<span class="comment__content">{{ comment.content }}</span>
				</div>
			</div>
			<span class="comment__date">{{ formatDate(comment.creationDate) }}</span>
			<div class="comment__actions">
				<b-icon-pencil class="comment__edit"></b-icon-pencil>
				<br />
				<b-icon-trash class="comment__delete" @click="deleteComment(comment)"></b-icon-trash>
			</div>
		</div>
	</div>
</template>

<script lang="js">
  import moment from 'moment';

  export default  {
    name: 'comment',
    props: ['comments'],
    methods: {
      formatDate(date){
        moment.locale('fr')
        return moment(String(date)).format('DD MMMM YYYY');
      },
      deleteComment(comment){
        this.$emit('commentDelete', comment);
      }
    },
}
</script>

<style scoped lang="scss">
h4 {
	margin-bottom: 10px;
}

.comment {
	background-color: #e5e5e5;
	border: 1px solid black;
	padding: 15px;
	height: 100%;

	&__card {
		border: 1px solid black;
		border-radius: 5px;
		background-color: #fff;
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 15px;
		box-shadow: 2px 3px 7px 0px #5f5f5f;
		padding: 20px;
	}

	&__info {
		text-align: left;
	}

	&__picture {
		margin-right: 15px;
	}

	&__author {
		margin-bottom: 0px;
		font-size: 14px;
	}

	&__content {
		font-size: 12px;
		white-space: nowrap;
	}

	&__date {
		font-size: 10px;
		white-space: nowrap;
		justify-self: flex-end;
		align-self: flex-end;
		position: relative;
		top: 18px;
		left: 15px;
	}

	&__actions {
		white-space: nowrap;
		right: 35px;
		position: absolute;
	}

	&__edit {
		color: #99d5c6;
		cursor: pointer;
	}

	&__delete {
		color: #d77270;
		cursor: pointer;
	}
}
</style>
