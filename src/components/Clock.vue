<template>
  <div class="clock">
    <div class="time">{{ time }}</div>
    <div class="date">Today is {{ date }}</div>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  data() {
    return {
      time: '',
      date: ''
    };
  },
  mounted() {
      this.start();
  },
  methods: {
    start() {
      var week = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
      var timerID = setInterval(this.start, 1000);
      var cd = new Date();
      this.time = this.formatTime(cd);//this.zeroPadding(cd.getHours(), 2) + ':' + this.zeroPadding(cd.getMinutes(), 2) + ':' + this.zeroPadding(cd.getSeconds(), 2);
      this.date = week[cd.getDay()] + ", " + this.zeroPadding(cd.getMonth()+1, 2) + "/" + this.zeroPadding(cd.getDate(), 2) + "/" + this.zeroPadding(cd.getFullYear(), 4);
    },
    formatTime(date) {
      var hours = date.getHours();
      var minutes = date.getMinutes();
      var ampm = hours >= 12 ? 'PM' : 'AM';
      hours = hours % 12;
      hours = hours ? hours : 12;
      // the hour '0' should be '12'

      minutes = minutes < 10 ? '0' + minutes : minutes;
      var strTime = hours + ':' + minutes + ' ' + ampm;


      return this.zeroPadding(hours, 2) + ':' + this.zeroPadding(minutes, 2) + ':' + this.zeroPadding(date.getSeconds(), 2) + " " + ampm;
    },
    zeroPadding(num, digit) {
      var zero = '';
      for(var i = 0; i < digit; i++) {
          zero += '0';
      }
      return (zero + num).slice(-digit);
    }
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
.time {
  letter-spacing: 0.05em;
  font-size: 80px;
  padding: 5px 0;
    }
.date {
  letter-spacing: 0.1em;
  font-size: 24px;
}
</style>
