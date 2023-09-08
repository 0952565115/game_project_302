<script setup>
//import HelloWorld from './components/HelloWorld.vue'
import { ref,} from 'vue'

const win_count_player1 = ref(0)
const draw_count_player1 = ref(0)
const loss_count_player1 = ref(0)

const win_count_player2 = ref(0)
const draw_count_player2 = ref(0)
const loss_count_player2 = ref(0)



const control_game = {
	'ค้อน': {
		'ค้อน': 'เสมอ',
		'กรรไกร': 'ชนะ',
    'กระดาษ': 'แพ้',
    'ความรัก': 'แพ้'
	},
  'กรรไกร': {
		'ค้อน': 'แพ้',
		'กรรไกร': 'เสมอ',
    'กระดาษ': 'ชนะ',
    'ความรัก': 'แพ้'
	},
	'กระดาษ': {
		'ค้อน': 'ชนะ',
		'กรรไกร': 'แพ้',
    'กระดาษ': 'เสมอ',
    'ความรัก': 'แพ้'
	},
  'ความรัก': {
		'ค้อน': 'ชนะ',
		'กรรไกร': 'ชนะ',
    'กระดาษ': 'ชนะ',
    'ความรัก': 'เสมอ'
	}
}



const player1_choose = ref('');
const player2_choose = ref('');
const result = ref('');

const choiceImages = {
  'ค้อน': 'https://cdn.discordapp.com/attachments/898851458068394004/1149365854719459359/hammer-pixel.png',
  'กรรไกร': 'https://media.discordapp.net/attachments/898851458068394004/1149365855721902230/scissor-pixel.png',
  'กระดาษ': 'https://media.discordapp.net/attachments/898851458068394004/1149365855512174732/paper-pixel.png',
  'ความรัก': 'https://media.discordapp.net/attachments/898851458068394004/1149365854966927370/hearts-pixel.gif',
};



function getRandomChoice() {
  const choices = ['ค้อน', 'กรรไกร', 'กระดาษ', 'ความรัก'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1_choose.value = getRandomChoice();
  player2_choose.value = getRandomChoice();

  const out_result = control_game[player1_choose.value][player2_choose.value];

  if (out_result === 'ชนะ') {
    win_count_player1.value++;
    loss_count_player2.value++;
    result.value = 'Player 1 ชนะ';
  } else if (out_result === 'แพ้') {
    win_count_player2.value++;
    loss_count_player1.value++;
    result.value = 'Player 2 ชนะ';
  } else {
    draw_count_player1.value++;
    draw_count_player2.value++;
    result.value = 'เสมอ';
  }
}

function reset_round() {
  player1_choose.value = '';
  player2_choose.value = '';
  result.value = '';
  win_count_player1.value = 0;
  draw_count_player1.value = 0;
  loss_count_player1.value = 0;
  win_count_player2.value = 0;
  draw_count_player2.value = 0;
  loss_count_player2.value = 0;
}

</script>

<template>
  <div class="contrainer_all">
    <div class="box_title">
			<div class="text_title">เกมเป่ายิ๊งฉุบ pixel</div>
    </div>

      <div class="contrainer_game">
        <div class="box_1" id="box_play_1">
          Player 1 : ได้ออก {{ player1_choose }} <br>
          <img v-if="!player1_choose" src="https://media.discordapp.net/attachments/898851458068394004/1149365855285690409/lucky-pixel.png" alt="Player 1 Default" class="box_img" />
          <img v-else :src="choiceImages[player1_choose]" alt="Player 1 Choice" class="box_img" />
          <!--<img v-if="player1_choose" :src="choiceImages[player1_choose]" alt="Player 1 Choice" class="box_img"/>-->
        </div>
        <div class="box_2" id="box_play_2">
          Player 2 : ได้ออก {{ player2_choose }} <br>
          <img v-if="!player2_choose" src="https://media.discordapp.net/attachments/898851458068394004/1149365855285690409/lucky-pixel.png" alt="Player 2 Default" class="box_img" />
          <img v-else :src="choiceImages[player2_choose]" alt="Player 2 Choice" class="box_img" />
          <!--<img v-if="player2_choose" :src="choiceImages[player2_choose]" alt="Player 2 Choice" class="box_img" />-->
        </div>
      </div>

    <div class="box_start_game">
      <button @click="display_answer" class="button_start_game"> เป่า...ยิ๊ง...ฉุบ... </button>
    </div>

  <div class="contrainer_score_all"> 
    <div class="contrainer_score_1">
      <div class="box_score"> ผลการแข่งขัน <br> {{ result }} </div>
      <!--<div class="box_score"> แต้มชนะ Player1 <br> {{ win_count_player1 }} </div>-->
      <!--<div class="box_score"> แต้มแพ้ Player1 <br> {{ loss_count_player1 }} </div>-->
      <!--<div class="box_score"> แต้มเสมอ Player1 <br>{{ draw_count_player1 }} </div>-->
    </div>
    <div class="contrainer_score_2">
      <div class="box_score"> แต้ม : Player1 <br> {{ win_count_player1 }} </div>
      <div class="box_score"> แต้ม : Player2 <br> {{ win_count_player2 }} </div>
      <!--<div class="box_score"> แต้มชนะ Player2 <br> {{ win_count_player2 }} </div>-->
      <!--<div class="box_score"> แต้มแพ้ Player2 <br> {{ loss_count_player2 }} </div>-->
      <!--<div class="box_score"> แต้มเสมอ Player2 <br>{{ draw_count_player2 }} </div>-->
    </div>
  </div> 
    <div class="box_new_game">
      <button @click="reset_round" class="button_new_game"> เริ่มเกมใหม่ </button>
    </div>

  </div>    

</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Charmonman:wght@700&family=Poppins:wght@400;500;600;700&display=swap');


/*ALl body*/
:root {
  font-family: 'Charmonman', cursive;
  font-size: 24px;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: #242424;
  /*background-color: #ffffff;*/
  background-image: url("https://cdn.discordapp.com/attachments/898851458068394004/1149383610755989554/pixel-green-background.gif");
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;

}

#app {
  max-width: 1280px;
  margin:  auto;
  padding: 1rem;
  text-align: center;
}

*{
  padding: 10px;
}


/* -----contrainer_all----- */
.contrainer_all {
  /*background-image: linear-gradient( 135deg, #CE9FFC 10%, #7367F0 100%);*/
  background-color: rgba(106, 134, 104, 0.4);
  border-radius: 20px;
}


/* -----main topic----- */
.box_title {
  background-image: linear-gradient( 135deg, #FDF1A1 10%, #F6AEC5 100%);
  width: 450px;
  height: 50px;
  margin: auto;
  display: flex;
  /*align-items: center;*/
  justify-content: center;
  border-radius: 15px;
}

.text_title {
  font-size: 32px;
  margin-top: -4px;
  /*color: #ffffff;*/
  /*text-shadow: 2px 2px 4px #000000;*/
}


/* -----contrainer_game----- */
.contrainer_game {
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-content: center;
  backdrop-filter: blur(2px);
  box-shadow: 2px 2px 20px 5px rgba(53, 67, 52, 0.4);
  border-radius: 20px;
  color: #ffffff;
  margin-left: 200px;
  margin-right: 200px;
  margin-top: 20px;
  padding: 20px;
}

.box_1 {
  margin-right: 25px;
  width: 275px;
  height: 175px;
  text-shadow: 2px 2px 4px #000000;
}

.box_2 {
  margin-left: 25px;
  width: 275px;
  height: 175px;
  text-shadow: 2px 2px 4px #000000;
}

.box_img {
  width: 100px;
  height: 100px; 
}


/* -----button_start_game----- */
.button_start_game {
  padding: 20px;
  width: 215px;
  height: 60px;
  background-image: linear-gradient( 135deg, #BFEB88 10%, #5DC264 100%);
  border-radius: 10px;
  border: 1px solid transparent;
  font-size: 24px;
  font-weight: 400;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  margin: auto; 
  display: flex;
  align-items: center;
  justify-content: center;
  padding-bottom: 10px;
  /*transition: border-color 0.25s;*/
}

.button_start_game:hover {
  box-shadow: 2px 2px 20px 5px rgba(53, 67, 52, 0.5);
  transform:translate(0px, -5px) ;
  transition: 0.5s;
  padding: 15px;
  padding-bottom: 10px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient( 135deg, #F3D0E2 10%, #BEAED2 100%);
}

.box_start_game {
  display: flex;
  justify-content: center;
  align-items: center; 
  margin-top: 20px;
  margin-bottom: 20px;
}


/* -----contrainer_score_all----- */
.contrainer_score_all{
  margin-left: 100px;
  margin-right: 100px;
  height: 210px;
  color: #ffffff;
  backdrop-filter: blur(2px);
  box-shadow: 2px 2px 20px 5px rgba(53, 67, 52, 0.5);
  border-radius: 20px;
  /*border:3px solid #ffffff;*/
}

.contrainer_score_1 {

  text-shadow: 2px 2px 4px #000000;
}

.contrainer_score_2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  text-shadow: 2px 2px 4px #000000;
}


/* -----button_new_game----- */
.button_new_game {
  width: 165px;
  height: 60px;
  background-image: linear-gradient( 135deg, #83D1D4 1%, #878BCD 100%);
  border-radius: 10px;
  border: 1px solid transparent;
  font-size: 24px;
  font-weight: 400;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
  padding-top: 9px;
}

.button_new_game:hover {
  box-shadow: 2px 2px 20px 5px rgba(53, 67, 52, 0.5);
  transform:translate(0px, -5px) ;
  transition: 0.5s;
  padding: 15px;
  padding-top: 9px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient( 135deg, #F6AEC5 10%, #f05770 100%);
}

.box_new_game {
  display: flex;
  justify-content: center;
  align-items: center; 
  margin-top: 20px;
  margin-bottom: 10px;
}

</style>