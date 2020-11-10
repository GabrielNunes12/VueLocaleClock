<template>
  <div class="lolcatClone">
    <h4>
      I CAN HAZ TIME?? <br>
      <span id="clock">{{time}}</span>
    </h4>
     <img id="lolcatImage" src="https://s3.amazonaws.com/media.skillcrush.com/skillcrush/wp-content/uploads/2016/08/normalTime.jpg" alt="lolcat">
     <blockquote id="timeEvent">This is where time events are reported</blockquote>

     <!-- Wakeup -->
     <h3>Set Wake Up Time</h3>
     <select class="wakeUpTimeSelector" v-for="(localTime, indexTime) in wakeUpTime" :key="indexTime">
       <option value="" disabled selected>Select a time</option>
       <option value="morning" v-for="(localTimeSelector, indexTimeSelector) in localTime.morning" :key="indexTimeSelector">{{localTimeSelector}}</option>
     </select>

     <!-- Lunch -->
     <h3> Lunch </h3>
     <select class="lunchTimeSelector" v-for="(localTime, indexTime) in wakeUpTime" :key="indexTime">
       <option value="" disabled selected> Select a time to lunch</option>
       <option value="lunch" v-for="(localTimeSelector,indexLocalTimeSelector) in localTime.lunchTime" :key="indexLocalTimeSelector">{{localTimeSelector}}</option>
     </select>

     <!-- Nap -->
     <h3> Nap </h3>
     <select class="napTimeSelector" v-for="(localTime, indexTime) in wakeUpTime" :key="indexTime">
       <option value="" disabled selected> Select a time to take a nap</option>
       <option value="nap" v-for="(localTimeSelectorNap, indexNapTime) in localTime.napTime" :key="indexNapTime">{{localTimeSelectorNap}}</option>
     </select>
    <br>
    <button id="partyTimeButton">Party!</button>
    <button @click="showCurrentTime" id="partyTimeButton">Show current time!</button>
    <footer>
      <p>&copy; Gabriel 2020</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  data(){
    return{
      wakeUpTime: [{
        morning:['1 AM - 2AM','2 AM - 3AM','3 AM - 4AM','4 AM - 5AM','5 AM - 6AM','6 AM - 7AM','7 AM - 8AM','8 Am - 9 Am', '9 AM - 10AM','10 AM - 11AM','11 AM - 12PM'],
        lunchTime: ['12 PM - 1PM','1 PM - 2PM','2 PM - 3PM','3 PM - 4PM','4 PM - 5 PM','5 PM - 6 PM','6 PM - 7PM','7 PM - 8PM', '8 PM - 9PM','9 PM - 10PM','10 PM - 11PM','11 PM - 12AM','12 AM - 1AM'],
        napTime: ['1 PM - 2PM','2 PM - 3PM','3 PM - 4PM','4 PM - 5 PM','5 PM - 6 PM','6 PM - 7PM','7 PM - 8PM', '8 PM - 9PM','9 PM - 10PM','10 PM - 11PM','11 PM - 12AM','12 AM - 1AM']
      }],
      noon: 0,
      partytime: '',
      evening: 0,
    }
  },
   methods: {
      showCurrentTime()
      {
          // display the string on the webpage
          const clock = document.getElementById('clock');
      
          let currentTime = new Date();
      
          let hours = currentTime.getHours();
          let minutes = currentTime.getMinutes();
          let seconds = currentTime.getSeconds();
          let meridian = "AM";
      
          if (hours >= this.noon)
          {
            meridian = "PM";
          }

          if (hours > this.noon)
          {
            hours = hours - 12;
          }
      
          if (minutes < 10)
          {
              minutes = "0" + minutes;
          }
          if (seconds < 10)
          {
              seconds = "0" + seconds;
          }
          const clockTime = `${hours}:${minutes}:${seconds}${meridian}!`;
      
          return clock.innerText = clockTime
      },
     
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.lolcatClone {
  font: 14px/26px 'Bungee', Helvetica, Arial, sans-serif;
  color: #222;
  margin: 0px;
  padding: 0px;
  text-transform: uppercase;
}
h4 #clock {
  font-size: 36px;
  display: block;
  padding: 5px 0px;
}

#lolcatImage {
  max-width:30em
}

blockquote {
  font: 2em/1em 'Open Sans', sans-serif;
  -webkit-text-stroke: 1px black;
  text-shadow: 2px 2px #000;
  margin: -80px 0 100px 0;
  color: #fff;
}
blockquote:before { content: '"'; }
blockquote:after { content: '"'; }

#lolcat {
  margin: 0 auto;
  -webkit-border-radius: 100px;
  -moz-border-radius: 100px;
  border-radius: 10px;
  border:10px solid #222;
}

#wakeUpTimeSelector, #lunchTimeSelector, #napTimeSelector {
  padding: 10px 0;
}

#partyTimeButton {
  background-color: #222;
  width: 300px;
  font-family: 'Bungee', cursive;
  font-size: 18px;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px 0;
  margin-top: 20px;
}

footer p {
  text-transform: uppercase;
  font-size: 12px;
}

h3 {
  margin: 40px 0 0;
}
</style>
