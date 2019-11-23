<template>
	<div>
		<div class="scoreBoard">
			<span>O победил {{wins.O}} раз</span>
			<h2>Табло</h2>
			<span>X победил {{wins.X}} раз</span>
		</div>
		<div id="app">
			<div id="details">
				<h1>Tic Tac Toe</h1>
				<h2>Раунд №{{matches + 1}}</h2>
			</div>
			<grid></grid>
			<button class="restart" @click="restart">Перезапуск</button>
		</div>
	</div>
</template>

<script>
import Grid from './components/Grid.vue'

export default {
	components: { Grid },
  name: 'app',
  data () {
    return {
      matches: 0,
			wins: {
				O: 0,
				X: 0
			}
    }
  },
	created()
	{
		Event.$on('win', winner => this.wins[winner]++);
	},
	methods: {
		restart()
		{
			Event.$emit('clearCell');
			Event.$emit('gridReset');
			this.matches++;
		}
	}
}
</script>

<style>
	body
	{
		background-color: #fff;
		color: #fff;
		font-family: 'Dosis', sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		margin: 0;
	}
	#app
	{
		margin: 0 auto;
		max-width: 270px;
		color: #34495e;

	}
	h1
	{
		text-transform: uppercase;
		font-weight: bold;
		font-size: 3em;
	}
	.restart
	{
		background-color: #e74c3c;
		color: #fff;
		border: 0;
		border-bottom-left-radius: 10px;
		border-bottom-right-radius: 10px;
		font-family: 'Dosis', sans-serif;
		font-size: 1.4em;
		font-weight: bold;
		margin: 0;
		padding: 15px;
		width: 100%;
	}
	.restart:hover
	{
		background-color:#c0392b;
		cursor: pointer;
	}
	.scoreBoard
	{
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		width: 100%;
		height: 15px;
		background-color: #16a085;
		box-sizing: border-box;
		padding: 20px;
		overflow: hidden;
	}
	.scoreboard h2
	{
		margin: 0;
	}
	.scoreBoard span
	{
		float: right;
		font-size: 1.5em;
		font-weight: bold;
		margin-left: 20px;
	}
</style>
