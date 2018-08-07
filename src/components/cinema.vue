<template>
  <div class="hello">

    <div class="cinema-container">

      <div class="cinema cinema-block">
        <div><h2>Cinema</h2></div>
        <div v-for="line in seats" class="seats-line" >
          <div v-for="seat in line" class="seat" v-on:click="selectSeat(seat)" v-bind:class="returnSeatColor(seat)">
            L:{{seat.line}} S:{{seat.seat}}
          </div>
        </div>
      </div>

      <div v-if="selectedSeats.length" >
        Tickets you select:

          <p v-for="ticket in selectedSeats">
            The line: {{ticket.line}}, the seat: {{ticket.seat}}
          </p>

        <p>Total cost: {{selectedSeats.length * 100}} rub</p>
        <button v-on:click="reserveSeats()">Buy tickets</button>
        <button v-on:click="cancelSelected()">Cancel</button>
      </div>
      <div v-if="showThanksMessage">
        <h1>Thanks for your order</h1>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'cinema',
  props: {

  },
  data () {
      return {
          seats: [
              [{line: 1, seat: 1, isFree: true},
                  {line: 1, seat: 2, isFree: false},
                  {line: 1, seat: 3, isFree: true},
                  {line: 1, seat: 4, isFree: true},
                  {line: 1, seat: 5, isFree: true},
                  {line: 1, seat: 6, isFree: true},
                  {line: 1, seat: 7, isFree: true},
                  {line: 1, seat: 8, isFree: true},
                  {line: 1, seat: 9, isFree: true},
                  {line: 1, seat: 10, isFree: true}],
              [{line: 2, seat: 1, isFree: true},
                  {line: 2, seat: 2, isFree: true},
                  {line: 2, seat: 3, isFree: true},
                  {line: 2, seat: 4, isFree: false},
                  {line: 2, seat: 5, isFree: true},
                  {line: 2, seat: 6, isFree: true},
                  {line: 2, seat: 7, isFree: true},
                  {line: 2, seat: 8, isFree: true},
                  {line: 2, seat: 9, isFree: true},
                  {line: 2, seat: 10, isFree: true}],
              [{line: 3, seat: 1, isFree: true},
                  {line: 3, seat: 2, isFree: true},
                  {line: 3, seat: 3, isFree: true},
                  {line: 3, seat: 4, isFree: false},
                  {line: 3, seat: 5, isFree: true},
                  {line: 3, seat: 6, isFree: true},
                  {line: 3, seat: 7, isFree: true},
                  {line: 3, seat: 8, isFree: true},
                  {line: 3, seat: 9, isFree: true},
                  {line: 3, seat: 10, isFree: true}],
              [{line: 4, seat: 1, isFree: true},
                  {line: 4, seat: 2, isFree: true},
                  {line: 4, seat: 3, isFree: true},
                  {line: 4, seat: 4, isFree: true},
                  {line: 4, seat: 5, isFree: false},
                  {line: 4, seat: 6, isFree: true},
                  {line: 4, seat: 7, isFree: true},
                  {line: 4, seat: 8, isFree: true},
                  {line: 4, seat: 9, isFree: true},
                  {line: 4, seat: 10, isFree: true}],
              [{line: 5, seat: 1, isFree: true},
                  {line: 5, seat: 2, isFree: true},
                  {line: 5, seat: 3, isFree: true},
                  {line: 5, seat: 4, isFree: true},
                  {line: 5, seat: 5, isFree: true},
                  {line: 5, seat: 6, isFree: true},
                  {line: 5, seat: 7, isFree: true},
                  {line: 5, seat: 8, isFree: true},
                  {line: 5, seat: 9, isFree: true},
                  {line: 5, seat: 10, isFree: true}]
          ],
          selectedSeats: [],
          showThanksMessage: false,
      }
  },
    methods:  {
        afterLaunch: function() {
          console.log('cinema is running');
        },
        selectSeat: function(seat) {
          if(!seat.isFree) return;
          if(this.selectedSeats.indexOf(seat) !== -1) {
              this.selectedSeats.splice(this.selectedSeats.indexOf(seat), 1);
          } else {
              this.selectedSeats.push(seat);
          }
        },
        returnSeatColor: function(seat) {
          if(this.selectedSeats.indexOf(seat) !== -1) {
              return 'selected-seat';
          } else {
              return seat.isFree ? 'free-seat' : 'occupied-seat';
          }
        },
        reserveSeats: function() {
          let cntxt = this;
          for(let i=0; i<cntxt.seats.length; i++) {
              for(let s=0; s<cntxt.seats[i].length; s++) {
                  if(cntxt.selectedSeats.indexOf(cntxt.seats[i][s]) !== -1) {
                      cntxt.seats[i][s].isFree = false;
                  }
              }
          }
          cntxt.selectedSeats = [];
          cntxt.showThanksMessage = true;
          setTimeout(function(){
            cntxt.showThanksMessage = false;
          }, 2000)
        },
        cancelSelected: function() {
            this.selectedSeats = [];
        }
    },
    mounted() {
      this.afterLaunch();
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }

  .cinema-container {
    display: flex;
  }

  .cinema-block {
    margin-left: 50px;
    margin-right: 50px;
  }
  .cinema {
    display: flex;
    flex-direction: column;
    background-color: #dcdbdb;
    padding: 50px;
  }

  .seats-line {
    display: flex;
  }

  .seat {
    margin: 5px;
    height: 50px;
    width: 50px;
    color: white;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  .free-seat {
    background-color: green;
  }

  .selected-seat {
    background-color: grey;
  }

  .occupied-seat {
    background-color: red;
  }


</style>
