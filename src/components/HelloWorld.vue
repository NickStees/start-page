<template>
  <div class="hello">
    <div class="container">
      <h1>{{ msg }}</h1>
      <div class="row">
        <div class="col-sm-6">
          <div id="time"></div>
          <div id="date"></div>
        </div>
        <div class="col-sm-6 text-right">
          <div id="weather">Loading&hellip;</div>
          <div id="details">Waiting for Dark Sky&hellip;</div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-3"><img src="https://picsum.photos/150" class="img-thumb" alt=""></div>
        <div class="col-md-3"><img src="https://picsum.photos/150" class="img-thumb" alt=""></div>
        <div class="col-md-3"><img src="https://picsum.photos/150" class="img-thumb" alt=""></div>
        <div class="col-md-3"><img src="https://picsum.photos/150" class="img-thumb" alt=""></div>
      </div>
      <hr>
      <div class="row">
        <div class="col-md-4">
          <h3>Links</h3>
          <ul>
            <li><a href="#">Link - Click</a></li>
            <li><a href="#">Link - Click</a></li>
            <li><a href="#">Link - Click</a></li>
          </ul>
        </div>
        <div class="col-md-4">
          <h3>Links</h3>
          <ul>
            <li><a href="#">Link - Click</a></li>
            <li><a href="#">Link - Click</a></li>
            <li><a href="#">Link - Click</a></li>
          </ul>
        </div>
        <div class="col-md-4">
          <h3>Links</h3>
          <ul>
            <li><a href="#">Link - Click</a></li>
            <li><a href="#">Link - Click</a></li>
            <li><a href="#">Link - Click</a></li>
          </ul>
        </div>
      </div>
    </div>
    <div class="no-print">
      Cards:{{cardsLength}}
      <button v-on:click="clearCards">clearCards</button>
    </div>

    <div class="bingo-card" v-for="card in arrCards">
      <div class="cell" v-for="item in card"><span>{{item}}</span></div>
    </div>


  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Custom Start Page',
      cards: [
          'one'
      ],
      arrCards: [
          'one',
          'two',
          'three'
      ]
    }
  },
  beforeMount:function(){
    // startTime();
  },
  mounted:function(){
    startTime();
  },
  methods:{
     getTerms:function(){
       var terms = [
         'Reboot',
         'Ask Mary',
         'Windows 10'
       ];
       return terms;
     },
     saveCard:function (card){
       // save the card
        var newcards = JSON.parse(localStorage.getItem('cards'));

        var newarrCards = JSON.parse(localStorage.getItem('arrCards'));

        if(!newarrCards){
          newarrCards = [];
        }
        this.arrCards.push(card);

        if(newcards){
          newcards.push(card.join());
        }else{
          newcards = [card.join()];
        }
        localStorage.setItem('cards', JSON.stringify(newcards));
        localStorage.setItem('arrCards', JSON.stringify(this.arrCards));

     },
     getCards:function (){
       // save the card
       var newarrCards =  JSON.parse(localStorage.getItem('arrCards'));
       if(!newarrCards){
         newarrCards = [];
       }
       this.arrCards = newarrCards;
       return JSON.parse(localStorage.getItem('cards'));
     },
     clearCards:function(){
       localStorage.removeItem('cards');
       localStorage.removeItem('arrCards');
       this.arrCards = [];
       this.cards = this.getCards();
     }

  },
  computed: {
    // a computed getter
    cardsLength: function () {
      // `this` points to the vm instance
      if(this.cards){
        return this.cards.length;
      }else{
        return 0;
      }
    }
  },
  updated: function() {
    // stuff to run after vue is done
    // Finds current time and date, formats it properly

	},

}
function startTime() {
	var monthNames = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
	var dayNames   = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
	var now  = new Date();
	var time = [now.getHours(), now.getMinutes(), now.getSeconds()];
	var date = [now.getDate(), now.getDay(), now.getMonth(), now.getFullYear()];
	var hour = time[0];
	var mins = time[1];
	var secs = time[2];
	var ampm = hour >= 12 ? 'PM' : 'AM';
	var day  = date[0];
	var weekday = dayNames[date[1]];
	var month = monthNames[date[2]];
	var year = date[3];
	hour = hour % 12;
	hour = hour ? hour : 12;
	mins = mins < 10 ? '0' + mins : mins;
	secs = secs < 10 ? '0' + secs : secs;
	document.getElementById('time').innerHTML = hour + ':' + mins + ':' + secs + ' ' + ampm;
	document.getElementById('date').innerHTML = weekday + ', ' + month + ' ' + day + ', ' + year;
	var t = setTimeout(startTime, 500);
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #42b983;
}

</style>
