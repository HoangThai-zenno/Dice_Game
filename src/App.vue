<template>
	<div id="app">
		<div class="wrapper clearfix">
			<players v-bind:scorePlayers="scorePlayers" v-bind:activePlayer="activePlayer"
				v-bind:curentScore="curentScore" />

			<controls v-on:handleNewGame="handleNewGame" v-on:handleRollDice="handleRollDice"
				v-on:handleHoldScore="handleHoldScore" />

			<dices v-bind:dices="dices" />

			<popup-rule v-bind:isOpenPopup="isOpenPopup" v-on:handleConfirm="handleConfirm" />
		</div>
	</div>
</template>

<script>
import Players from './components/Players.vue';
import Controls from './components/Controls.vue';
import Dices from './components/Dices.vue';
import PopupRule from './components/PopupRule.vue';
export default {
	name: 'app',
	data() {
		return {
			isPlaying: false,
			isOpenPopup: false,
			activePlayer: 0,
			scorePlayers: [18, 26],
			curentScore: 10,
			dices: [1, 6]
		}
	},
	methods: {

		nextPlayer() {
			this.activePlayer = this.activePlayer === 0 ? 1 : 0;
			this.curentScore = 0;
		},
		handleHoldScore() {
			if(this.isPlaying){

				let { curentScore, scorePlayers, activePlayer } = this;
				let oldScore = scorePlayers[activePlayer];
				this.$set(this.scorePlayers, activePlayer, oldScore + curentScore);
				this.nextPlayer();
			}
			else{
				alert("Please click new game");
			}


		},
		handleNewGame() {
			this.isOpenPopup = true;
		},
		handleRollDice() {
			if (this.isPlaying) {
				var dice1 = Math.floor(Math.random() * 6) + 1;
				var dice2 = Math.floor(Math.random() * 6) + 1;
				console.log(dice1, dice2)
				this.dices = [dice1, dice2];
				if (dice1 === 1 || dice2 === 1) {
					let player = this.activePlayer + 1
					setTimeout(function () {
						alert(`Player ${player} đã quay trúng xúc sắc số 1. Rất tiếc!`)
					}, 10);
					this.nextPlayer();
				}
				else {
					this.curentScore = this.curentScore + dice1 + dice2;
				}
			}
			else {
				alert("Please click new game");
			}
		},
		handleConfirm() {
			this.isPlaying = true;
			this.isOpenPopup = false;
			this.activePlayer = 0;
			this.curentScore = 0;
			this.scorePlayers = [0, 0];
			this.dices = [1, 1];
		}
	},
	components: {
		Players,
		Controls,
		Dices,
		PopupRule
	}
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;

}

.clearfix::after {
	content: "";
	display: table;
	clear: both;
}

body {
	background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/back.jpg');
	background-size: cover;
	background-position: center;
	font-family: Lato;
	font-weight: 300;
	position: relative;
	height: 100vh;
	color: #555;
}

.wrapper {
	width: 1000px;
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	background-color: #fff;
	box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
	overflow: hidden;
}
</style>
