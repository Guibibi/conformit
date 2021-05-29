<template lang="html">
	<div class="comment">
		<h4>Commentaires</h4>
		<div v-for="comment in comments" :key="comment" class="comment__card">
			{{ comment.author }}
			{{ comment.creationDate }}
			{{ comment.content }}
		</div>
	</div>
</template>

<script lang="js">

  export default  {
    name: 'comment',
    props: ['comments'],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}
</script>

<style scoped lang="scss">
.comment {
	background-color: #e5e5e5;
	border: 1px solid black;
	padding: 15px;
}
</style>
